---
title: Ubuntu for Linux 基础练习 
date: 2025-11-18
tag: 练习
categories: Linux
---

# Ubuntu for Linux 基础练习

## Ubuntu操作练习

**基础操作**

1. ### 用户和权限管理

   - 创建新用户`testuser`并设置密码
   - 将该用户添加到`sudo`组
   - 创建一个共享目录`/home/shared`,设置权限775，确保该组用户有读写权限

   ```bash
   ### 相关操作
   
   # 创建用户组zdffgroup
   sudo groupadd zdffgroup
   # 创建用户testuser并将其加入zdffgroup组
   sudo useradd -m -g zdffgroup -s /bin/bash testuser
   # 设置用户testuser密码
   sudo passwd testuser
   # 给testuser用户授予管理员权限
   sudo usermod -aG sudo testuser
   # 创建一个共享目录`/home/shared`,设置权限775，确保该组用户有读写权限
   sudo mkdir /home/shared
   sudo chown :zdffgroup /home/shared/
   sudo chmod 775 /home/shared
   
   
   
   "
   创建用户之前创建用户组是属于同一组的用户以便共享文件权限，当创建用户时，不指定组，Linux会自动创建一个与用户名同名的组作为该用户的主组。
   
   sudo useradd -m -g zdffgroup -s /bin/bash testuser
   -m 或 --create-home 在创建用户的同时，为用户创建家目录
   -g 指定新用户所属的主组
   -s /bin/bash 为用户指定默认的登录Shell
   
   sudo usermod -aG sudo testuser
   -G 指定要添加的附加组
   -a append（追加）的意思，将用户添加到指定的附加组中，而不影响用户已有的其他附加组
   "
   ```

   ![image-20251122081110019](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20251122081110019.png)

2. ### 软件包管理

   - 使用apt更新软件包列表
   - 安装`nginx web`服务器
   - 配置`nginx`开机自启，并启动服务
   - 使用`systemctl`检查服务状态

   ```bash
   sudo apt update
   sudo apt install nginx -y
   sudo systemctl start nginx
   sudo systemctl enable nginx
   systemctl status nginx
   ```

   ![image-20251122082511577](C:\Users\ccxx\AppData\Roaming\Typora\typora-user-images\image-20251122082511577.png)

3. ### 进程和系统监控

   - 使用`htop`监控系统资源
   - 查找占用CPU最高的进程
   - 使用`journalctl`查看系统日志
   - 设置一个定时任务，每天凌晨3点清理临时文件

   ```bash
   # 使用htop
   htop
   "
   htop 界面说明
   上部：CPU使用率、内存使用情况、交换空间、负载平均值
   中部：进程列表，显示PID、用户、优先级、CPU%、内存%、进程命令
   下部：功能键提示
   "
   # 查找占用CPU最高的进程
   ps aux --sort=-%cpu | head -11
   ### 使用journalctl查看系统日志
   # 查看所有日志
   sudo journalctl
   # 查看最近的日志并实时刷新
   sudo journalctl -f
   # 查看指定服务的日志
   sudo journalctl -u nginx.service
   sudo journalctl -u docker.service
   ```

   ```
   # 创建脚本文件
   sudo vim /usr/local/bin/cleanup_temp.sh
   
   ### 添加以下内容：
   #!/bin/bash
   # 清理临时文件脚本
   
   echo "$(date): 开始清理临时文件" >> /var/log/cleanup.log
   
   # 清理 /tmp 目录（保留最近7天的文件）
   find /tmp -type f -atime +7 -delete 2>/dev/null
   
   # 清理用户缓存
   find /home -type f -name "*.tmp" -atime +30 -delete 2>/dev/null
   find /home -type f -name "*.log" -atime +30 -delete 2>/dev/null
   
   # 清理包管理器缓存
   # apt-get clean
   
   # 清理系统日志（保留最近30天）
   find /var/log -name "*.log" -type f -mtime +30 -delete
   
   echo "$(date): 临时文件清理完成" >> /var/log/cleanup.log
   ```

   **给脚本执行权限**

   ```bash
   sudo chmod +x /usr/local/bin/cleanup_temp.sh
   ```

   **设置定时任务（cron）**

   ```bash
   # 编辑root的crontab（推荐用于系统任务）
   sudo crontab -e
   ```

   **添加定时任务**

   在crontab文件中添加：

   ```bash
   # 每天凌晨3点执行清理脚本
   0 3 * * * /usr/local/bin/cleanup_temp.sh
   ```

   **验证定时任务**

   ```bash
   # 查看当前用户的定时任务
   crontab -l
   # 查看root的定时任务
   sudo crontab -l
   # 查看cron执行日志（Ubuntu）
   sudo grep CRON /var/log/syslog
   # 或者查看脚本自己的日志
   sudo tail -f /var/log/cleanup.log
   ```

4. ### 网络配置

   - 查看网络接口信息
   - 测试到8.8.8.8的网络连通性
   - 使用netstat查看监听端口
   - 配置UFW防火墙，开放80和443端口

   ```bash
   # 查看网络接口信息
   ip a 或者 ip addr
   # 测试到8.8.8.8的网络连通性
   ping -c 4 8.8.8.8
   # 使用netstat查看监听端口
   sudo netstat -tulpn
   # 配置UFW防火墙，开放80和443端口
   sudo ufw allow 80/tcp
   sudo ufw allow 443/tcp
   ```

5. ### 磁盘管理

   - 检查磁盘使用情况
   - 查找大于100MB的文件
   - 创建一个2GB的交换文件并启用
   - 设置磁盘空间监控告警

   ```bash
   # 检查磁盘使用情况
   df -h
   # 查找大于100MB的文件
   sudo find / -type f -size +100M -printf "%s %p\n" 2>/dev/null | sort -nr
   "
   find / 从根目录开始查找文件
   -type f 只查找普通文件（排除目录、设备文件等）
   -size +100M 查找大小超过100MB的文件
   -printf "%s %p\n" 自定义输出格式： %s: 文件大小（字节） %p: 完整文件路径 \n: 换行符
   2>/dev/null 将错误信息（如权限拒绝）重定向到空设备，不显示错误
   | sort -nr sort -n: 按数值排序 -r: 反向排序（从大到小）
   "
   ```

   ```text
   ### 创建一个2GB的交换文件并启用
   1. 创建交换文件
   # 检查当前交换空间
   free -h
   swapon --show
   # 创建2GB的交换文件（bs=1M count=2048 或 bs=1G count =2）
   sudo dd if=/dev/zero of=/swapfile bs=1M count=2048
   2. 设置权限
   sudo chmod 600 /swapfile
   3. 格式化为交换空间
   sudo mkswap /swapfile
   4. 启用交换文件
   sudo swapon /swapfile
   # 验证交换文件已启用
   free -h
   swapon --show
   5. 永久生效（重启后仍然有效）
   # 备份fstab文件
   sudo cp /etc/fstab /etc/fstab.bak
   # 将交换文件添加到fstab
   echo '/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
   ```

   ```text
   #### 设置磁盘空间监控告警
   ### 使用Shell脚本 + Cron
   1. 创建监控脚本
   # 创建脚本目录
   sudo mkdir -p /usr/local/scripts
   sudo vim /usr/local/scripts/disk_alert.sh
   2.脚本内容
   #!/bin/bash
   # 磁盘空间监控告警脚本
   
   # 配置参数
   THRESHOLD=90        # 警告阈值（百分比）
   EMAIL=""  # 接收告警的邮箱
   LOG_FILE="/var/log/disk_alert.log"
   
   # 获取磁盘使用率
   DISK_USAGE=$(df / | awk 'NR==2 {print $5}' | sed 's/%//')
   
   # 获取主机名
   HOSTNAME=$(hostname)
   
   # 记录日志
   echo "$(date): 检查磁盘使用率 - ${DISK_USAGE}%" >> $LOG_FILE
   
   # 检查是否超过阈值
   if [ $DISK_USAGE -gt $THRESHOLD ]; then
       # 记录告警
       echo "$(date): 警告！磁盘使用率 ${DISK_USAGE}% 超过阈值 ${THRESHOLD}%" >> $LOG_FILE
       
       # 发送邮件告警（需要配置邮件系统）
       echo "警告：服务器 $HOSTNAME 的根分区磁盘使用率已达到 ${DISK_USAGE}%，请及时清理！" | \
       mail -s "磁盘空间告警 - $HOSTNAME" $EMAIL
       
       # 发送到系统日志
       logger -t disk_alert "磁盘使用率 ${DISK_USAGE}% 超过阈值"
   fi
   3. 设置脚本权限和定时任务
   # 给脚本执行权限
   sudo chmod +x /usr/local/scripts/disk_alert.sh
   # 添加到cron，每30分钟检查一次
   sudo crontab -e
   # 添加以下行：
   */30 * * * * /usr/local/scripts/disk_alert.sh
   ```

## Shell脚本编写练习

**脚本练习**

```text
# SHELL脚本知识点
1. cut
用途: 按列或定界符提取文本内容
简单、速度快、但功能有限。适合固定分隔符的文本。
基本语法: cut -d "<分隔符>" -f <列号>
-d 指定字段分隔符（默认是TAB）
-f 指定输出第几列，可以用逗号指定多列，比如-f1,3
# 假设输出 df -h | head -2
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        50G   20G   28G  42% /

# 取第二列（Size）
df -h | head -2 | tail -1 | cut -d' ' -f2
空格不规则时，cut 不好用，因为它只按固定分隔符。

2. awk
用途: 按列、按模式提取和处理文本
比cut强大， 可以做条件判断、计算、格式化输出
默认以空格或TAB分列。
基本语法: awk '/匹配模式/ {print $列号}'
free -h | awk '/Mem:/ {print $2}'
/Mem:/ → 匹配包含 Mem: 的行
{print $2} → 输出第二列

df -h | awk '$6=="/" {print $4}'
$6 是挂载点列，$6=="/" → 找根分区
{print $4} → 输出第四列（Avail）

echo -e "1\n2\n3" | awk '{sum+=$1} END {print sum}'
awk 列号 $1, $2, ...
也可以用 $0 表示整行

3. sed
用途: 流编辑器，用于替换、删除、插入、提取行等。
功能强大，常用于批量修改文本。
基本语法:
sed '命令' 文件
常用命令:
1. 替换
echo "hello world" | sed 's/world/shell/'
# 输出: hello shell
2. 删除行
# 删除第1行
sed '1d' file.txt
3. 打印匹配行
# 打印包含 "Mem:" 的行
free -h | sed -n '/Mem:/p'
4. 删除多余空格
echo "   hello   world  " | sed 's/^ *//;s/ *$//;s/  */ /g'
# 输出: hello world
```

1. ### 系统信息收集脚本

   ```bash
   # 编写脚本收集：系统版本、内存使用、磁盘空间、登录用户等
   # 输出格式化的报告到文件
   #!/bin/bash
   
   # 系统信息收集脚本
   # 作者:ccxx
   # 日期: $(date)
   
   # 定义颜色（可选， 用于终端显示）
   RED='\033[0;31m'
   GREEN='\033[0;32m'
   YELLOW='\033[1;33m'
   NC='\033[0m'  # 没有颜色
   
   # 定义输出文件
   REPORT_FILE="system_report_$(date +%Y%m%d_%H%M%S).txt"
   
   # 函数： 添加章节标题
   add_section() {
       echo "" >> $REPORT_FILE
       echo "=== $1 ===" >> $REPORT_FILE
       echo "--------------------------------" >> $REPORT_FILE
   }
   
   # 生成报告头
   echo "===============================" > $REPORT_FILE
   echo "			系统信息报告" >> $REPORT_FILE
   echo "===============================" >> $REPORT_FILE
   echo "生成时间: $(date)" >> $REPORT_FILE
   echo "主机名: $(hostname)" >> $REPORT_FILE
   echo "===============================" >> $REPORT_FILE
   
   # 系统信息
   add_section "系统版本信息"
   echo "操作系统: " >> $REPORT_FILE
   if [ -f /etc/os-release ]; then
   	source /etc/os-release
   	echo " - 名称: $NAME" >> $REPORT_FILE
   	echo " - 版本: $VERSION" >> $REPORT_FILE
   	echo " - ID: $ID" >> $REPORT_FILE
   fi
   echo "内核版本: $(uname -r)" >> $REPORT_FILE
   echo "系统架构: $(uname -m)" >> $REPORT_FILE
   
   # 内存信息
   add_section "内存使用情况"
   free -h | sed 's/^ *//' >> $REPORT_FILE
   
   # 磁盘信息
   add_section "磁盘空间信息"
   df -h | sed 's/^ *//' >> $REPORT_FILE
   
   # 用户信息
   add_section "登录用户信息"
   echo "当前用户数: $(who | wc -l)" >> $REPORT_FILE
   who | sed 's/^ *//' >> $REPORT_FILE
   
   # 系统负载
   add_section "系统负载信息"
   uptime | sed 's/^ *//' >> $REPORT_FILE
   
   # CPU信息
   add_section "CPU信息"
   echo "CPU型号: $(grep "model name" /proc/cpuinfo | head -1 | cut -d: -f2 | sed 's/^*//')" >> $REPORT_FILE
   
   echo "" >> $REPORT_FILE
   echo "==================================" >> $REPORT_FILE
   echo "报告生成完成: $REPORT_FILE" >> $REPORT_FILE
   
   # 在终端显示成功信息
   echo -e "${GREEN}系统信息报告已生成： ${YELLOW}$REPORT_FILE${NC}"
   echo -e "${GREEN}报告内容预览：${NC}"
   echo "=================================="
   head -20 $REPORT_FILE
   ```

2. ### 日志分析脚本

   ```bash
   # 分析/var/log/syslog，统计ERROR和WARNING出现次数
   # 提取包含特定关键词的日志行
   # 生成每日报告
   #!/bin/bash
   
   # 日志分析脚本
   # 功能：分析syslog，统计错误和警告，提取关键词，生成报告
   
   LOG_FILE="/var/log/syslog"
   REPORT_DIR="/var/log/reports"
   DATE=$(date +%Y-%m-%d)
   REPORT_FILE="$REPORT_DIR/syslog_report_$DATE.txt"
   
   # 创建报告目录
   mkdir -p "$REPORT_DIR"
   
   # 检查日志文件是否存在
   if [ ! -f "$LOG_FILE" ]; then
       echo "错误: 日志文件 $LOG_FILE 不存在!"
       exit 1
   fi
   
   # 生成报告头部
   echo "=== 系统日志分析报告 ($DATE) ===" > "$REPORT_FILE"
   echo "生成时间: $(date)" >> "$REPORT_FILE"
   echo "日志文件: $LOG_FILE" >> "$REPORT_FILE"
   echo "======================================" >> "$REPORT_FILE"
   echo "" >> "$REPORT_FILE"
   
   # 1. 统计ERROR和WARNING出现次数
   echo "1. 错误和警告统计:" >> "$REPORT_FILE"
   echo "-------------------" >> "$REPORT_FILE"
   
   ERROR_COUNT=$(grep -i "ERROR" "$LOG_FILE" | wc -l)
   WARNING_COUNT=$(grep -i "WARNING" "$LOG_FILE" | wc -l)
   
   echo "ERROR 出现次数: $ERROR_COUNT" >> "$REPORT_FILE"
   echo "WARNING 出现次数: $WARNING_COUNT" >> "$REPORT_FILE"
   echo "" >> "$REPORT_FILE"
   
   # 2. 提取包含特定关键词的日志行
   echo "2. 关键词相关日志:" >> "$REPORT_FILE"
   echo "-------------------" >> "$REPORT_FILE"
   
   # 定义要搜索的关键词数组
   KEYWORDS=("fail" "failed" "critical" "timeout" "denied" "refused" "crash" "exception")
   
   for keyword in "${KEYWORDS[@]}"; do
       count=$(grep -i "$keyword" "$LOG_FILE" | wc -l)
       if [ $count -gt 0 ]; then
           echo "关键词 '$keyword' 出现次数: $count" >> "$REPORT_FILE"
       fi
   done
   echo "" >> "$REPORT_FILE"
   
   # 3. 显示最近的ERROR和WARNING日志
   echo "3. 最近的ERROR日志 (最近10条):" >> "$REPORT_FILE"
   echo "-------------------------------" >> "$REPORT_FILE"
   grep -i "ERROR" "$LOG_FILE" | tail -10 >> "$REPORT_FILE"
   echo "" >> "$REPORT_FILE"
   
   echo "4. 最近的WARNING日志 (最近10条):" >> "$REPORT_FILE"
   echo "--------------------------------" >> "$REPORT_FILE"
   grep -i "WARNING" "$LOG_FILE" | tail -10 >> "$REPORT_FILE"
   echo "" >> "$REPORT_FILE"
   
   # 4. 按服务/进程统计
   echo "5. 按进程统计ERROR和WARNING:" >> "$REPORT_FILE"
   echo "----------------------------" >> "$REPORT_FILE"
   echo "进程名 | ERROR数 | WARNING数" >> "$REPORT_FILE"
   echo "------|---------|----------" >> "$REPORT_FILE"
   
   # 提取所有包含ERROR或WARNING的进程
   grep -E -i "ERROR|WARNING" "$LOG_FILE" | awk '{print $5}' | sed 's/\[\|\]\|://g' | sort | uniq | while read process; do
       if [ -n "$process" ]; then
           error_count=$(grep -i "ERROR" "$LOG_FILE" | grep "$process" | wc -l)
           warning_count=$(grep -i "WARNING" "$LOG_FILE" | grep "$process" | wc -l)
           if [ $error_count -gt 0 ] || [ $warning_count -gt 0 ]; then
               printf "%-15s | %8d | %9d\n" "$process" "$error_count" "$warning_count" >> "$REPORT_FILE"
           fi
       fi
   done
   
   echo "" >> "$REPORT_FILE"
   echo "报告生成完成: $REPORT_FILE"
   
   # 显示报告摘要
   echo ""
   echo "=== 报告摘要 ==="
   echo "ERROR总数: $ERROR_COUNT"
   echo "WARNING总数: $WARNING_COUNT"
   echo "详细报告: $REPORT_FILE"
   ```

3. ### 备份脚本

   ```bash
   # 创建目录备份脚本，支持：
   # - 增量备份
   # - 保留最近7天的备份
   # - 备份完成后发送邮件通知
   
   
   #!/bin/bash
   # 目录备份脚本
   # 功能：增量备份、保留最近7天备份、邮件通知
   
   # 配置区域 - 根据实际环境修改这些变量
   SOURCE_DIR="/path/to/source"          # 要备份的源目录
   BACKUP_BASE="/path/to/backups"        # 备份存储基目录
   BACKUP_NAME="daily_backup"            # 备份名称前缀
   RETENTION_DAYS=7                      # 保留天数
   LOG_FILE="/var/log/backup.log"        # 日志文件路径
   
   # 邮件通知配置
   EMAIL_RECIPIENT="admin@example.com"   # 收件人邮箱
   EMAIL_SUBJECT="备份完成通知"          # 邮件主题
   
   # 创建时间戳
   TIMESTAMP=$(date +%Y%m%d_%H%M%S)
   TODAY=$(date +%Y%m%d)
   BACKUP_DIR="${BACKUP_BASE}/${BACKUP_NAME}_${TODAY}"
   
   # 日志函数
   log() {
       echo "[$(date '+%Y-%m-%d %H:%M:%S')] $1" | tee -a "$LOG_FILE"
   }
   
   # 错误处理函数
   error_exit() {
       log "错误: $1"
       send_notification "失败" "$1"
       exit 1
   }
   
   # 发送邮件通知函数
   send_notification() {
       local status="$1"
       local message="$2"
       
       cat << EOF | mail -s "${EMAIL_SUBJECT} - ${status}" "$EMAIL_RECIPIENT"
   备份任务执行完成
   
   状态: ${status}
   时间: $(date)
   源目录: ${SOURCE_DIR}
   备份目录: ${BACKUP_DIR}
   备份时间: ${TIMESTAMP}
   
   详细信息:
   ${message}
   
   日志文件: ${LOG_FILE}
   
   EOF
       log "邮件通知已发送至: ${EMAIL_RECIPIENT}"
   }
   
   # 检查依赖
   check_dependencies() {
       local deps=("rsync" "mail" "find")
       for dep in "${deps[@]}"; do
           if ! command -v "$dep" &> /dev/null; then
               error_exit "缺少必要工具: $dep"
           fi
       done
   }
   
   # 检查目录是否存在
   check_directories() {
       if [ ! -d "$SOURCE_DIR" ]; then
           error_exit "源目录不存在: $SOURCE_DIR"
       fi
       
       if [ ! -d "$BACKUP_BASE" ]; then
           log "创建备份基目录: $BACKUP_BASE"
           mkdir -p "$BACKUP_BASE" || error_exit "无法创建备份基目录"
       fi
   }
   
   # 查找最新的完整备份（用于增量备份参考）
   find_latest_backup() {
       find "$BACKUP_BASE" -maxdepth 1 -type d -name "${BACKUP_NAME}_*" | grep -v "$BACKUP_DIR" | sort | tail -n 1
   }
   
   # 执行备份
   perform_backup() {
       local latest_backup=$(find_latest_backup)
       local link_dest=""
       
       if [ -n "$latest_backup" ]; then
           link_dest="--link-dest=$latest_backup"
           log "执行增量备份，参考备份: $latest_backup"
       else
           log "执行首次完整备份"
       fi
       
       # 创建备份目录
       mkdir -p "$BACKUP_DIR" || error_exit "无法创建备份目录"
       
       # 使用rsync进行增量备份
       log "开始备份..."
       rsync -avh --delete $link_dest "$SOURCE_DIR/" "$BACKUP_DIR/" >> "$LOG_FILE" 2>&1
       
       if [ $? -eq 0 ]; then
           log "备份完成: $BACKUP_DIR"
           # 创建备份完成标记文件
           echo "备份时间: $TIMESTAMP" > "$BACKUP_DIR/backup.info"
           echo "备份类型: $([ -n "$link_dest" ] && echo "增量" || echo "完整")" >> "$BACKUP_DIR/backup.info"
           echo "源目录: $SOURCE_DIR" >> "$BACKUP_DIR/backup.info"
       else
           error_exit "备份过程中出现错误"
       fi
   }
   
   # 清理旧备份
   cleanup_old_backups() {
       log "清理超过 ${RETENTION_DAYS} 天的旧备份..."
       
       # 查找并删除旧备份
       find "$BACKUP_BASE" -maxdepth 1 -type d -name "${BACKUP_NAME}_*" -mtime +$RETENTION_DAYS | while read -r old_backup; do
           if [ -n "$old_backup" ] && [ "$old_backup" != "$BACKUP_DIR" ]; then
               log "删除旧备份: $old_backup"
               rm -rf "$old_backup"
           fi
       done
       
       log "旧备份清理完成"
   }
   
   # 生成备份报告
   generate_report() {
       local backup_size=$(du -sh "$BACKUP_DIR" 2>/dev/null | cut -f1)
       local total_backups=$(find "$BACKUP_BASE" -maxdepth 1 -type d -name "${BACKUP_NAME}_*" | wc -l)
       
       cat << EOF
   === 备份报告 ===
   备份状态: 成功
   备份时间: $(date)
   源目录: $SOURCE_DIR
   目标目录: $BACKUP_DIR
   备份大小: $backup_size
   备份类型: $([ -n "$(find_latest_backup)" ] && echo "增量" || echo "完整")
   保留策略: ${RETENTION_DAYS} 天
   当前备份数量: $total_backups
   磁盘使用情况:
   $(df -h "$BACKUP_BASE")
   
   EOF
   }
   
   # 主函数
   main() {
       log "=== 开始备份任务 ==="
       
       # 检查依赖
       check_dependencies
       
       # 检查目录
       check_directories
       
       # 执行备份
       perform_backup
       
       # 清理旧备份
       cleanup_old_backups
       
       # 生成报告并发送通知
       local report=$(generate_report)
       log "$report"
       send_notification "成功" "$report"
       
       log "=== 备份任务完成 ==="
   }
   
   # 脚本入口
   if [ $# -eq 0 ]; then
       # 无参数时执行备份
       main
   else
       case $1 in
           "--cleanup-only")
               # 仅执行清理
               check_dependencies
               check_directories
               cleanup_old_backups
               ;;
           "--report")
               # 生成报告
               generate_report
               ;;
           "--help")
               # 显示帮助
               echo "用法: $0 [选项]"
               echo "选项:"
               echo "  无参数    执行完整备份流程"
               echo "  --cleanup-only  仅清理旧备份"
               echo "  --report        生成备份报告"
               echo "  --help         显示此帮助信息"
               ;;
           *)
               echo "未知参数: $1"
               echo "使用 --help 查看使用方法"
               exit 1
               ;;
       esac
   fi
   ```
   
   
   
4. ### 用户管理脚本

   ```bash
   # 批量创建用户，从CSV文件读取用户名和密码
   # 设置用户配额
   # 生成创建报告
   ```

5. ### 服务监控脚本

   ```bash
   # 监控指定服务（如nginx、mysql）状态
   # 如果服务停止，自动重启并发送告警
   # 记录监控日志
   ```

   

## Python脚本编写练习

**Python练习**

1. ### 系统信息收集工具

   ```bash
   # 使用psutil库收集系统信息
   # 输出CPU、内存、磁盘、网络使用情况
   # 生成HTML格式报告
   
   #!/usr/bin/env python3
   # -*- coding: utf-8 -*-
   
   import os
   import psutil
   import datetime
   from jinja2 import Template
   
   
   # ================================
   # 数据采集层：所有采集函数统一封装
   # ================================
   
   class Collector:
   
       @staticmethod
       def cpu():
           freq = psutil.cpu_freq()
           return {
               "physical": psutil.cpu_count(logical=False),
               "logical": psutil.cpu_count(logical=True),
               "frequency": freq.current if freq else 0,
               "usage": psutil.cpu_percent(interval=1),
               "per_cpu": psutil.cpu_percent(interval=1, percpu=True),
           }
   
       @staticmethod
       def memory():
           mem = psutil.virtual_memory()
           swap = psutil.swap_memory()
           gb = 1024**3
           return {
               "total": round(mem.total / gb, 2),
               "used": round(mem.used / gb, 2),
               "available": round(mem.available / gb, 2),
               "percent": mem.percent,
               "swap_total": round(swap.total / gb, 2),
               "swap_used": round(swap.used / gb, 2),
               "swap_percent": swap.percent
           }
   
       @staticmethod
       def disks():
           gb = 1024**3
           disks = []
           for p in psutil.disk_partitions():
               try:
                   u = psutil.disk_usage(p.mountpoint)
                   disks.append({
                       "device": p.device,
                       "mount": p.mountpoint,
                       "fs": p.fstype,
                       "total": round(u.total / gb, 2),
                       "used": round(u.used / gb, 2),
                       "free": round(u.free / gb, 2),
                       "percent": u.percent
                   })
               except PermissionError:
                   continue
           return disks
   
       @staticmethod
       def network():
           io = psutil.net_io_counters()
           mb = 1024**2
           return {
               "sent_mb": round(io.bytes_sent / mb, 2),
               "recv_mb": round(io.bytes_recv / mb, 2),
               "sent_packets": io.packets_sent,
               "recv_packets": io.packets_recv,
           }
   
       @staticmethod
       def system():
           boot = datetime.datetime.fromtimestamp(psutil.boot_time())
           return {
               "boot": boot.strftime("%Y-%m-%d %H:%M:%S"),
               "uptime": str(datetime.datetime.now() - boot).split('.')[0],
               "timestamp": datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S"),
           }
   
   
   # ================================
   # HTML 模板层（高美观，可随时替换）
   # ================================
   
   REPORT_TEMPLATE = r"""
   <!DOCTYPE html>
   <html lang="zh-cn">
   <head>
   <meta charset="UTF-8">
   <title>系统监控报告</title>
   
   <style>
   body {
       font-family: 'Segoe UI', Arial;
       margin: 0;
       padding: 25px;
       background: #f5f6fa;
   }
   .container {
       max-width: 1200px;
       margin: auto;
   }
   h1 {
       text-align: center;
       padding: 25px;
       background: linear-gradient(135deg, #6a11cb, #2575fc);
       color: white;
       border-radius: 12px;
       box-shadow: 0 4px 12px rgba(0,0,0,.1);
   }
   .section {
       background: white;
       padding: 20px;
       border-radius: 12px;
       margin-top: 25px;
       box-shadow: 0 2px 8px rgba(0,0,0,0.06);
   }
   .section-title {
       border-left: 6px solid #6a11cb;
       padding-left: 12px;
       margin-bottom: 15px;
       font-size: 1.4em;
   }
   .grid {
       display: grid;
       grid-template-columns: repeat(auto-fit,minmax(260px,1fr));
       gap: 18px;
   }
   .card {
       background: #fafbfc;
       padding: 15px;
       border-left: 5px solid #2575fc;
       border-radius: 8px;
   }
   .label { font-weight: bold; color: #555; }
   .value { margin-top: 6px; font-size: 1.2em; color: #333; }
   .progress {
       height: 9px; background: #ddd; border-radius: 5px; margin-top: 8px;
   }
   .fill {
       height: 100%; border-radius: 5px;
       background: linear-gradient(90deg,#6a11cb,#2575fc);
   }
   .warning { color: #e84118; font-weight: bold; }
   
   table {
       width: 100%; border-collapse: collapse;
   }
   th, td {
       padding: 10px; border-bottom: 1px solid #eee;
   }
   th { background: #f0f0f5; }
   tr:hover { background: #f9f9f9; }
   
   .footer {
       text-align: center;
       margin-top: 25px;
       color: #888;
   }
   </style>
   
   </head>
   <body>
   <div class="container">
   
   <h1>系统监控报告</h1>
   
   <div class="section">
       <div class="section-title">系统信息</div>
       <div class="grid">
           <div class="card"><div class="label">启动时间</div><div class="value">{{ sys.boot }}</div></div>
           <div class="card"><div class="label">系统已运行</div><div class="value">{{ sys.uptime }}</div></div>
           <div class="card"><div class="label">生成时间</div><div class="value">{{ sys.timestamp }}</div></div>
       </div>
   </div>
   
   <div class="section">
       <div class="section-title">CPU 信息</div>
       <div class="grid">
           <div class="card"><div class="label">物理核心</div><div class="value">{{ cpu.physical }}</div></div>
           <div class="card"><div class="label">逻辑核心</div><div class="value">{{ cpu.logical }}</div></div>
           <div class="card"><div class="label">当前频率</div><div class="value">{{ cpu.frequency }} MHz</div></div>
   
           <div class="card">
               <div class="label">CPU 使用率</div>
               <div class="value {% if cpu.usage > 80 %}warning{% endif %}">{{ cpu.usage }}%</div>
               <div class="progress"><div class="fill" style="width:{{ cpu.usage }}%"></div></div>
           </div>
       </div>
   </div>
   
   <div class="section">
       <div class="section-title">内存信息</div>
       <div class="grid">
           <div class="card"><div class="label">总内存</div><div class="value">{{ mem.total }} GB</div></div>
           <div class="card"><div class="label">已使用</div><div class="value">{{ mem.used }} GB</div></div>
           <div class="card"><div class="label">可用</div><div class="value">{{ mem.available }} GB</div></div>
   
           <div class="card">
               <div class="label">使用率</div>
               <div class="value {% if mem.percent > 80 %}warning{% endif %}">{{ mem.percent }}%</div>
               <div class="progress"><div class="fill" style="width:{{ mem.percent }}%"></div></div>
           </div>
       </div>
   
       <div class="card" style="margin-top:20px;">
           <div class="label">Swap 内存</div>
           <div class="value">{{ mem.swap_used }} GB / {{ mem.swap_total }} GB ({{ mem.swap_percent }}%)</div>
           <div class="progress"><div class="fill" style="width:{{ mem.swap_percent }}%"></div></div>
       </div>
   </div>
   
   <div class="section">
       <div class="section-title">磁盘信息</div>
       <table>
           <tr><th>设备</th><th>挂载点</th><th>文件系统</th><th>总(GB)</th><th>已使用</th><th>剩余</th><th>使用率</th></tr>
   
           {% for d in disks %}
           <tr>
               <td>{{ d.device }}</td>
               <td>{{ d.mount }}</td>
               <td>{{ d.fs }}</td>
               <td>{{ d.total }}</td>
               <td>{{ d.used }}</td>
               <td>{{ d.free }}</td>
               <td {% if d.percent > 85 %}class="warning"{% endif %}>{{ d.percent }}%</td>
           </tr>
           {% endfor %}
       </table>
   </div>
   
   <div class="section">
       <div class="section-title">网络信息</div>
       <div class="grid">
           <div class="card"><div class="label">发送数据</div><div class="value">{{ net.sent_mb }} MB</div></div>
           <div class="card"><div class="label">接收数据</div><div class="value">{{ net.recv_mb }} MB</div></div>
           <div class="card"><div class="label">发送包</div><div class="value">{{ net.sent_packets }}</div></div>
           <div class="card"><div class="label">接收包</div><div class="value">{{ net.recv_packets }}</div></div>
       </div>
   </div>
   
   <div class="footer">
       系统监控报告已生成 | 提示：超过 80% 使用率将标记为警告
   </div>
   
   </div>
   </body>
   </html>
   """
   
   
   # ================================
   # 生成报告
   # ================================
   
   class Report:
   
       @staticmethod
       def generate(filename="system_report.html"):
           data = {
               "cpu": Collector.cpu(),
               "mem": Collector.memory(),
               "disks": Collector.disks(),
               "net": Collector.network(),
               "sys": Collector.system(),
           }
   
           html = Template(REPORT_TEMPLATE).render(**data)
           with open(filename, "w", encoding="utf-8") as f:
               f.write(html)
   
           return filename
   
   
   # ================================
   # 主程序入口
   # ================================
   
   if __name__ == "__main__":
       print("正在生成报告…")
       output = Report.generate()
       print("生成完成:", os.path.abspath(output))
   ```

2. ### 日志文件解析器

   ```python
   # 解析Apache/Nginx访问日志
   # 统计：访问量最多的IP、最受欢迎的页面、错误状态码
   # 可视化显示结果
   
   #!/usr/bin/env python3
   # -*- coding: utf-8 -*-
   import re
   import abc
   from dataclasses import dataclass
   from typing import Iterator, Optional, Dict, List
   import collections
   import argparse
   import sys
   import matplotlib.pyplot as plt
   
   
   # ---------------------------------------------------------
   # 数据结构：使用 dataclass 表示一条结构化日志
   # ---------------------------------------------------------
   @dataclass
   class LogRecord:
       ip: str
       timestamp: str
       method: str
       url: str
       protocol: str
       status: int
       size: int
   
   
   # ---------------------------------------------------------
   # 抽象日志格式解析器（策略模式）
   # ---------------------------------------------------------
   class BaseLogFormat(abc.ABC):
       @abc.abstractmethod
       def parse(self, line: str) -> Optional[LogRecord]:
           pass
   
   
   # ---------------------------------------------------------
   # Three concrete log format implementations
   # ---------------------------------------------------------
   class CombinedLogFormat(BaseLogFormat):
       _pattern = re.compile(
           r'(\S+) (\S+) (\S+) \[(.*?)\] "(\S+) (\S+) (\S+)" (\d+) (\d+) "([^"]*)" "([^"]*)"'
       )
   
       def parse(self, line: str) -> Optional[LogRecord]:
           m = self._pattern.match(line)
           if not m:
               return None
           try:
               return LogRecord(
                   ip=m.group(1),
                   timestamp=m.group(4),
                   method=m.group(5),
                   url=m.group(6),
                   protocol=m.group(7),
                   status=int(m.group(8)),
                   size=int(m.group(9)),
               )
           except (IndexError, ValueError):
               return None
   
   
   class CommonLogFormat(BaseLogFormat):
       _pattern = re.compile(
           r'(\S+) (\S+) (\S+) \[(.*?)\] "(\S+) (\S+) (\S+)" (\d+) (\d+)'
       )
   
       def parse(self, line: str) -> Optional[LogRecord]:
           m = self._pattern.match(line)
           if not m:
               return None
           try:
               return LogRecord(
                   ip=m.group(1),
                   timestamp=m.group(4),
                   method=m.group(5),
                   url=m.group(6),
                   protocol=m.group(7),
                   status=int(m.group(8)),
                   size=int(m.group(9)),
               )
           except Exception:
               return None
   
   
   class NginxLogFormat(BaseLogFormat):
       _pattern = re.compile(
           r'(\S+) - (\S+) \[(.*?)\] "(\S+) (\S+) (\S+)" (\d+) (\d+) "([^"]*)" "([^"]*)"'
       )
   
       def parse(self, line: str) -> Optional[LogRecord]:
           m = self._pattern.match(line)
           if not m:
               return None
           try:
               return LogRecord(
                   ip=m.group(1),
                   timestamp=m.group(3),
                   method=m.group(4),
                   url=m.group(5),
                   protocol=m.group(6),
                   status=int(m.group(7)),
                   size=int(m.group(8)),
               )
           except Exception:
               return None
   
   
   # ---------------------------------------------------------
   # 日志读取器：流式解析
   # ---------------------------------------------------------
   class LogReader:
       def __init__(self, filepath: str, fmt: BaseLogFormat):
           self.filepath = filepath
           self.fmt = fmt
   
       def records(self) -> Iterator[LogRecord]:
           with open(self.filepath, "r", encoding="utf-8", errors="ignore") as f:
               for line in f:
                   rec = self.fmt.parse(line.strip())
                   if rec:
                       yield rec
   
   
   # ---------------------------------------------------------
   # 统计器：插件式，可扩展
   # ---------------------------------------------------------
   class LogStatistics:
       def __init__(self):
           self.total = 0
           self.ip = collections.Counter()
           self.urls = collections.Counter()
           self.status = collections.Counter()
   
       def feed(self, rec: LogRecord):
           self.total += 1
           self.ip[rec.ip] += 1
           self.urls[rec.url] += 1
           self.status[rec.status] += 1
   
       @property
       def errors(self) -> Dict[int, int]:
           return {k: v for k, v in self.status.items() if k >= 400}
   
   
   # ---------------------------------------------------------
   # 可视化模块：与统计模块完全解耦
   # ---------------------------------------------------------
   class LogVisualizer:
       def __init__(self, stats: LogStatistics):
           self.s = stats
   
       def draw(self, save_path=None):
           fig, axes = plt.subplots(2, 2, figsize=(14, 12))
           fig.suptitle("访问日志分析", fontsize=16, fontweight="bold")
   
           self._bar_chart(axes[0, 0], self.s.ip, "访问最多的 IP")
           self._bar_chart(axes[0, 1], self.s.urls, "最热门页面")
           self._bar_chart(axes[1, 0], self.s.status, "HTTP 状态码分布")
           self._bar_chart(axes[1, 1], self.s.errors, "错误状态码")
   
           plt.tight_layout()
   
           if save_path:
               plt.savefig(save_path, dpi=300, bbox_inches="tight")
           plt.show()
   
       def _bar_chart(self, ax, counter, title):
           items = counter.most_common(8)
           if not items:
               ax.set_title(title)
               ax.text(0.5, 0.5, '无数据', ha='center', va='center')
               return
   
           labels, counts = zip(*items)
           ax.bar(labels, counts)
           ax.set_title(title)
           ax.tick_params(axis="x", rotation=45)
   
   
   # ---------------------------------------------------------
   # CLI 主流程
   # ---------------------------------------------------------
   def main():
       parser = argparse.ArgumentParser(description="高级日志分析器")
   
       parser.add_argument("file", help="日志文件")
       parser.add_argument("-f", "--format", choices=["combined", "common", "nginx"],
                           default="combined")
       parser.add_argument("-o", "--output", help="保存图表")
       parser.add_argument("--no-plot", action="store_true")
   
       args = parser.parse_args()
   
       fmt_class = {
           "combined": CombinedLogFormat,
           "common": CommonLogFormat,
           "nginx": NginxLogFormat,
       }[args.format]()
   
       reader = LogReader(args.file, fmt_class)
       stats = LogStatistics()
   
       for rec in reader.records():
           stats.feed(rec)
   
       # 输出统计
       print(f"总请求数：{stats.total}")
       print("最热门 IP：", stats.ip.most_common(5))
       print("最热门 URL：", stats.urls.most_common(5))
       print("状态码统计：", stats.status)
   
       if not args.no_plot:
           viz = LogVisualizer(stats)
           viz.draw(args.output)
   
   
   if __name__ == "__main__":
       main()
   ```

3. ### 文件同步工具

   ```python
   # 实现两个目录的同步
   # 支持单向/双向同步
   # 使用hash校验文件一致性
   # 生成同步报告
   #!/usr/bin/env python3
   """
   高级文件同步工具（专业级结构版本）
   - 采用目录快照（Directory Snapshot）模型
   - 支持单向、双向同步
   - 使用 blake3 作为文件内容校验
   - 具备冲突检测、操作层抽象、执行器分离（dry-run / real-run）
   - 可扩展、可测试、可维护
   """
   
   import os
   import shutil
   import argparse
   from pathlib import Path
   from dataclasses import dataclass
   from typing import Dict, List, Optional
   from datetime import datetime
   
   try:
       import blake3  # 现代高速哈希
       HASH_FUNC = lambda: blake3.blake3()
   except ImportError:
       import hashlib
       HASH_FUNC = lambda: hashlib.md5()
   
   
   # ---------------------------------------------------------
   # 数据模型
   # ---------------------------------------------------------
   
   @dataclass
   class FileMeta:
       hash: str
       size: int
       mtime: float
   
   
   @dataclass
   class FileAction:
       action: str       # copy / update / delete / conflict
       src: Optional[str]
       dst: Optional[str]
       relative: str
       note: str = ""
   
   
   # ---------------------------------------------------------
   # 目录快照：高级同步工具的核心抽象
   # ---------------------------------------------------------
   
   class DirectorySnapshot:
       def __init__(self, path: str):
           self.root = Path(path)
           self.files: Dict[str, FileMeta] = {}
   
       def build(self):
           for file_path in self.root.rglob("*"):
               if file_path.is_file():
                   rel = str(file_path.relative_to(self.root))
                   meta = self._read_file_meta(file_path)
                   self.files[rel] = meta
           return self
   
       @staticmethod
       def _hash_file(path: Path, chunk: int = 65536) -> str:
           h = HASH_FUNC()
           with path.open("rb") as f:
               for chunk_data in iter(lambda: f.read(chunk), b""):
                   h.update(chunk_data)
           return h.hexdigest()
   
       def _read_file_meta(self, f: Path) -> FileMeta:
           st = f.stat()
           h = self._hash_file(f)
           return FileMeta(hash=h, size=st.st_size, mtime=st.st_mtime)
   
   
   # ---------------------------------------------------------
   # 文件同步核心逻辑（不执行，只生成动作）
   # ---------------------------------------------------------
   
   class FileSyncPlanner:
       """
       负责比较两个目录快照，生成 sync plan（动作列表）
       """
   
       def __init__(self, s1: DirectorySnapshot, s2: DirectorySnapshot):
           self.s1 = s1
           self.s2 = s2
   
       def one_way(self):
           """生成从 s1 → s2 的操作计划"""
           actions: List[FileAction] = []
   
           src_files = self.s1.files
           dst_files = self.s2.files
   
           # 需要复制或更新的文件
           for rel, src_meta in src_files.items():
               if rel not in dst_files:
                   actions.append(FileAction("copy", str(self.s1.root), str(self.s2.root), rel))
               else:
                   dst_meta = dst_files[rel]
                   if src_meta.hash != dst_meta.hash:
                       actions.append(FileAction("update", str(self.s1.root), str(self.s2.root), rel))
   
           # 需要删除的文件
           for rel in dst_files.keys() - src_files.keys():
               actions.append(FileAction("delete", None, str(self.s2.root), rel))
   
           return actions
   
       def two_way(self):
           """生成双向同步计划（含冲突检测）"""
           actions: List[FileAction] = []
   
           s1f = self.s1.files
           s2f = self.s2.files
   
           all_files = set(s1f.keys()) | set(s2f.keys())
   
           for rel in all_files:
   
               f1 = s1f.get(rel)
               f2 = s2f.get(rel)
   
               # 双方都不存在（理论上不会出现）
               if f1 is None and f2 is None:
                   continue
   
               # 单方新增
               if f1 and not f2:
                   actions.append(FileAction("copy", str(self.s1.root), str(self.s2.root), rel))
                   continue
   
               if f2 and not f1:
                   actions.append(FileAction("copy", str(self.s2.root), str(self.s1.root), rel))
                   continue
   
               # 双方存在但 hash 不一致 → 需要冲突判断
               if f1.hash != f2.hash:
                   # 修改时间判断谁更新
                   if f1.mtime > f2.mtime:
                       actions.append(FileAction("update", str(self.s1.root), str(self.s2.root), rel, note="mtime win"))
                   elif f2.mtime > f1.mtime:
                       actions.append(FileAction("update", str(self.s2.root), str(self.s1.root), rel, note="mtime win"))
                   else:
                       # 同时修改 → 冲突
                       actions.append(FileAction(
                           "conflict",
                           str(self.s1.root),
                           str(self.s2.root),
                           rel,
                           note="both modified"
                       ))
   
           return actions
   
   
   # ---------------------------------------------------------
   # 执行层（能 dry-run 也能真正执行）
   # ---------------------------------------------------------
   
   class FileSyncExecutor:
       def __init__(self, dry_run=False):
           self.dry_run = dry_run
           self.logs: List[str] = []
   
       def run(self, actions: List[FileAction]):
           for a in actions:
               if a.action == "copy":
                   self._copy(a)
               elif a.action == "update":
                   self._copy(a)
               elif a.action == "delete":
                   self._delete(a)
               elif a.action == "conflict":
                   self._conflict(a)
   
           return self.logs
   
       def _copy(self, a: FileAction):
           src_file = Path(a.src) / a.relative
           dst_file = Path(a.dst) / a.relative
   
           self._ensure_dir(dst_file)
   
           msg = f"[COPY] {src_file} → {dst_file}"
           self.logs.append(msg)
           if not self.dry_run:
               shutil.copy2(src_file, dst_file)
   
       def _delete(self, a: FileAction):
           dst = Path(a.dst) / a.relative
           msg = f"[DELETE] {dst}"
           self.logs.append(msg)
           if not self.dry_run and dst.exists():
               dst.unlink()
   
       def _conflict(self, a: FileAction):
           msg = f"[CONFLICT] {a.relative}  note={a.note}"
           self.logs.append(msg)
           # 若不是 dry-run，可将冲突文件另外备份
           if not self.dry_run:
               conflict_dst = Path(a.dst) / (a.relative + ".conflict")
               shutil.copy2(Path(a.src) / a.relative, conflict_dst)
   
       @staticmethod
       def _ensure_dir(path: Path):
           path.parent.mkdir(parents=True, exist_ok=True)
   
   
   # ---------------------------------------------------------
   # CLI 层
   # ---------------------------------------------------------
   
   def main():
       parser = argparse.ArgumentParser(description="高级文件同步工具")
       parser.add_argument("src")
       parser.add_argument("dst")
       parser.add_argument("--mode", choices=["one-way", "two-way"], default="one-way")
       parser.add_argument("--dry-run", action="store_true")
   
       args = parser.parse_args()
   
       s1 = DirectorySnapshot(args.src).build()
       s2 = DirectorySnapshot(args.dst).build()
   
       planner = FileSyncPlanner(s1, s2)
       actions = planner.one_way() if args.mode == "one-way" else planner.two_way()
   
       executor = FileSyncExecutor(dry_run=args.dry_run)
       logs = executor.run(actions)
   
       print("\n".join(logs))
   
   
   if __name__ == "__main__":
       main()
   ```

4. ### 网络端口扫描器

   ```python
   # 扫描指定IP的端口开放情况
   # 多线程提高扫描速度
   # 识别常见服务
   # 输出扫描结果到CSV
   
   #!/usr/bin/env python3
   """
   网络端口扫描器
   支持多线程扫描、服务识别和CSV输出
   """
   
   import socket
   import threading
   import csv
   import time
   import argparse
   from queue import Queue
   from datetime import datetime
   
   # 常见端口服务映射
   COMMON_SERVICES = {
       21: "FTP", 22: "SSH", 23: "Telnet", 25: "SMTP", 53: "DNS",
       80: "HTTP", 110: "POP3", 111: "RPC", 135: "RPC", 139: "NetBIOS",
       143: "IMAP", 443: "HTTPS", 993: "IMAPS", 995: "POP3S",
       1723: "PPTP", 3306: "MySQL", 3389: "RDP", 5432: "PostgreSQL",
       5900: "VNC", 6379: "Redis", 27017: "MongoDB"
   }
   
   class PortScanner:
       def __init__(self, target, threads=100, timeout=2):
           self.target = target
           self.threads = threads
           self.timeout = timeout
           self.ports_queue = Queue()
           self.results = []
           self.lock = threading.Lock()
           
       def resolve_target(self):
           """解析目标主机名或IP地址"""
           try:
               ip = socket.gethostbyname(self.target)
               try:
                   hostname = socket.gethostbyaddr(ip)[0]
               except socket.herror:
                   hostname = "Unknown"
               return ip, hostname
           except socket.gaierror:
               print(f"错误：无法解析目标 {self.target}")
               return None, None
       
       def scan_port(self, port):
           """扫描单个端口"""
           sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
           sock.settimeout(self.timeout)
           
           try:
               result = sock.connect_ex((self.target, port))
               if result == 0:
                   service = self.get_service_info(port, sock)
                   with self.lock:
                       self.results.append({
                           'port': port,
                           'state': 'open',
                           'service': service,
                           'banner': self.get_banner(sock) if service != "Unknown" else ""
                       })
                   print(f"发现开放端口: {port}/tcp - {service}")
               sock.close()
           except Exception as e:
               pass
       
       def get_service_info(self, port, sock):
           """获取服务信息"""
           # 首先检查常见服务映射
           if port in COMMON_SERVICES:
               return COMMON_SERVICES[port]
           
           # 尝试通过端口号获取服务名
           try:
               service = socket.getservbyport(port, 'tcp')
               return service
           except (OSError, socket.error):
               return "Unknown"
       
       def get_banner(self, sock):
           """尝试获取服务banner信息"""
           try:
               sock.settimeout(1.0)
               # 发送一些常见协议的探测数据
               banner = sock.recv(1024).decode('utf-8', errors='ignore').strip()
               return banner[:100]  # 限制banner长度
           except:
               return ""
       
       def worker(self):
           """工作线程函数"""
           while True:
               try:
                   port = self.ports_queue.get(timeout=1)
                   self.scan_port(port)
                   self.ports_queue.task_done()
               except:
                   break
       
       def scan_ports(self, ports):
           """扫描端口范围"""
           print(f"开始扫描目标: {self.target}")
           print(f"线程数: {self.threads}, 超时: {self.timeout}秒")
           print("-" * 50)
           
           start_time = time.time()
           
           # 添加端口到队列
           for port in ports:
               self.ports_queue.put(port)
           
           # 启动工作线程
           threads = []
           for _ in range(self.threads):
               thread = threading.Thread(target=self.worker)
               thread.daemon = True
               thread.start()
               threads.append(thread)
           
           # 等待所有任务完成
           self.ports_queue.join()
           
           end_time = time.time()
           scan_duration = end_time - start_time
           
           print("-" * 50)
           print(f"扫描完成! 耗时: {scan_duration:.2f}秒")
           print(f"发现 {len(self.results)} 个开放端口")
           
           return self.results
       
       def save_to_csv(self, filename=None):
           """保存结果到CSV文件"""
           if not filename:
               timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
               filename = f"port_scan_{self.target}_{timestamp}.csv"
           
           try:
               with open(filename, 'w', newline='', encoding='utf-8') as csvfile:
                   fieldnames = ['port', 'state', 'service', 'banner']
                   writer = csv.DictWriter(csvfile, fieldnames=fieldnames)
                   
                   writer.writeheader()
                   for result in self.results:
                       writer.writerow(result)
               
               print(f"结果已保存到: {filename}")
               return filename
           except Exception as e:
               print(f"保存CSV文件时出错: {e}")
               return None
   
   def parse_ports(ports_str):
       """解析端口范围字符串"""
       ports = set()
       
       # 处理逗号分隔的端口列表和范围
       parts = ports_str.split(',')
       for part in parts:
           part = part.strip()
           if '-' in part:
               # 处理端口范围
               start, end = part.split('-')
               try:
                   start_port = int(start.strip())
                   end_port = int(end.strip())
                   ports.update(range(start_port, end_port + 1))
               except ValueError:
                   continue
           else:
               # 处理单个端口
               try:
                   ports.add(int(part))
               except ValueError:
                   continue
       
       return sorted(ports)
   
   def main():
       parser = argparse.ArgumentParser(description='网络端口扫描器')
       parser.add_argument('target', help='目标IP地址或主机名')
       parser.add_argument('-p', '--ports', default='1-1000', 
                          help='端口范围 (例如: 80,443, 1-1000, 默认: 1-1000)')
       parser.add_argument('-t', '--threads', type=int, default=100,
                          help='线程数 (默认: 100)')
       parser.add_argument('--timeout', type=float, default=2.0,
                          help='连接超时时间 (默认: 2秒)')
       parser.add_argument('-o', '--output', help='输出CSV文件名')
       parser.add_argument('--common', action='store_true',
                          help='只扫描常见端口')
       
       args = parser.parse_args()
       
       # 如果选择常见端口，使用预定义的端口列表
       if args.common:
           ports = list(COMMON_SERVICES.keys())
       else:
           ports = parse_ports(args.ports)
       
       if not ports:
           print("错误：未找到有效的端口范围")
           return
       
       print(f"准备扫描 {len(ports)} 个端口...")
       
       # 创建扫描器实例
       scanner = PortScanner(args.target, args.threads, args.timeout)
       
       # 解析目标
       ip, hostname = scanner.resolve_target()
       if not ip:
           return
       
       print(f"目标IP: {ip}")
       if hostname != "Unknown":
           print(f"目标主机名: {hostname}")
       
       # 执行扫描
       results = scanner.scan_ports(ports)
       
       # 显示结果摘要
       if results:
           print("\n开放端口列表:")
           print("端口\t状态\t服务")
           print("-" * 30)
           for result in sorted(results, key=lambda x: x['port']):
               print(f"{result['port']}\t{result['state']}\t{result['service']}")
       
       # 保存结果
       scanner.save_to_csv(args.output)
   
   if __name__ == "__main__":
       main()
   ```

5. ### 自动化部署脚本

   ```python
   # 从Git仓库拉取代码
   # 安装依赖包
   # 运行测试
   # 部署到指定目录
   # 重启相关服务
   
   #!/usr/bin/env python3
   """
   高级自动化部署脚本示例
   功能：
   - 从Git拉取代码（克隆或拉取）
   - 安装依赖（Python/Node.js/Ruby）
   - 运行测试
   - 部署到指定目录（带备份）
   - 重启服务
   """
   
   import sys
   import subprocess
   import logging
   import shutil
   from pathlib import Path
   from datetime import datetime
   from dataclasses import dataclass, field
   from typing import Optional, List
   import tempfile
   import argparse
   
   # ==========================
   # 配置管理
   # ==========================
   @dataclass
   class DeploymentConfig:
       git_repo: str
       deploy_dir: Path
       service_names: List[str] = field(default_factory=list)
       branch: str = "main"
       exclude_dirs: List[str] = field(default_factory=lambda: ['.git', '__pycache__', 'node_modules', '.pytest_cache'])
       backup_suffix_format: str = "%Y%m%d_%H%M%S"
   
   # ==========================
   # 部署主类
   # ==========================
   class Deployer:
       def __init__(self, config: DeploymentConfig):
           self.config = config
           self.logger = self._setup_logger()
           self.temp_dir = Path(tempfile.mkdtemp(prefix="deploy_tmp_"))
   
       # --------------------------
       # 日志初始化
       # --------------------------
       def _setup_logger(self) -> logging.Logger:
           logger = logging.getLogger("Deployer")
           logger.setLevel(logging.INFO)
           formatter = logging.Formatter('%(asctime)s - %(levelname)s - %(message)s')
   
           # 输出到控制台
           console = logging.StreamHandler(sys.stdout)
           console.setFormatter(formatter)
           logger.addHandler(console)
   
           # 输出到文件
           file_handler = logging.FileHandler("deployment.log")
           file_handler.setFormatter(formatter)
           logger.addHandler(file_handler)
           return logger
   
       # --------------------------
       # 命令执行
       # --------------------------
       def run_command(self, command: str, cwd: Optional[Path] = None, shell: bool = True) -> bool:
           """运行命令，捕获输出并记录日志"""
           self.logger.info(f"执行命令: {command}")
           try:
               result = subprocess.run(
                   command, cwd=cwd, shell=shell,
                   capture_output=True, text=True, check=True
               )
               if result.stdout:
                   self.logger.info(result.stdout.strip())
               if result.stderr:
                   self.logger.warning(result.stderr.strip())
               return True
           except subprocess.CalledProcessError as e:
               self.logger.error(f"命令执行失败: {e}")
               if e.stderr:
                   self.logger.error(e.stderr.strip())
               return False
   
       # --------------------------
       # Git拉取/克隆
       # --------------------------
       def update_repo(self) -> bool:
           if (self.temp_dir / ".git").exists():
               self.logger.info("检测到已有仓库，执行 git pull")
               return self.run_command("git pull", cwd=self.temp_dir)
           else:
               self.logger.info("克隆仓库到临时目录")
               return self.run_command(f"git clone -b {self.config.branch} {self.config.git_repo} {self.temp_dir}")
   
       # --------------------------
       # 安装依赖
       # --------------------------
       def install_dependencies(self) -> bool:
           """支持Python, Node.js, Ruby"""
           requirements = self.temp_dir / "requirements.txt"
           package_json = self.temp_dir / "package.json"
           gemfile = self.temp_dir / "Gemfile"
   
           if requirements.exists():
               self.logger.info("检测到 requirements.txt, 安装Python依赖")
               return self.run_command("pip install -r requirements.txt", cwd=self.temp_dir)
           elif package_json.exists():
               self.logger.info("检测到 package.json, 安装Node.js依赖")
               return self.run_command("npm install", cwd=self.temp_dir)
           elif gemfile.exists():
               self.logger.info("检测到 Gemfile, 安装Ruby依赖")
               return self.run_command("bundle install", cwd=self.temp_dir)
           else:
               self.logger.info("未检测到依赖文件，跳过依赖安装")
               return True
   
       # --------------------------
       # 运行测试
       # --------------------------
       def run_tests(self) -> bool:
           """尝试运行常见测试命令"""
           test_commands = [
               "pytest", "python -m pytest", "npm test",
               "bundle exec rspec", "phpunit", "./gradlew test", "mvn test"
           ]
           for cmd in test_commands:
               if self.run_command(cmd, cwd=self.temp_dir):
                   self.logger.info("测试成功")
                   return True
           self.logger.warning("未找到可用测试命令，跳过测试")
           return True
   
       # --------------------------
       # 部署到目标目录
       # --------------------------
       def deploy(self) -> bool:
           target = self.config.deploy_dir
           target.mkdir(parents=True, exist_ok=True)
           backup_dir = target.parent / f"{target.name}_backup_{datetime.now().strftime(self.config.backup_suffix_format)}"
   
           if any(target.iterdir()):
               self.logger.info(f"备份当前部署到 {backup_dir}")
               shutil.copytree(target, backup_dir)
   
           # 清空目标目录
           for item in target.iterdir():
               if item.name not in [backup_dir.name]:
                   if item.is_dir():
                       shutil.rmtree(item)
                   else:
                       item.unlink()
   
           # 拷贝新代码
           for item in self.temp_dir.iterdir():
               if item.name not in self.config.exclude_dirs:
                   dest = target / item.name
                   if item.is_dir():
                       shutil.copytree(item, dest)
                   else:
                       shutil.copy2(item, dest)
   
           self.logger.info("部署完成")
           return True
   
       # --------------------------
       # 重启服务
       # --------------------------
       def restart_services(self) -> bool:
           if not self.config.service_names:
               self.logger.info("未指定服务名称，跳过服务重启")
               return True
           for service in self.config.service_names:
               cmd_list = [
                   f"sudo systemctl restart {service}",
                   f"sudo service {service} restart",
               ]
               for cmd in cmd_list:
                   if self.run_command(cmd):
                       self.logger.info(f"服务 {service} 重启成功")
                       break
               else:
                   self.logger.error(f"服务 {service} 重启失败")
                   return False
           return True
   
       # --------------------------
       # 清理临时目录
       # --------------------------
       def cleanup(self):
           if self.temp_dir.exists():
               shutil.rmtree(self.temp_dir)
               self.logger.info(f"已清理临时目录 {self.temp_dir}")
   
       # --------------------------
       # 执行完整部署
       # --------------------------
       def run(self) -> bool:
           steps = [
               ("更新代码", self.update_repo),
               ("安装依赖", self.install_dependencies),
               ("运行测试", self.run_tests),
               ("部署代码", self.deploy),
               ("重启服务", self.restart_services)
           ]
   
           for name, func in steps:
               self.logger.info(f"=== 执行步骤: {name} ===")
               if not func():
                   self.logger.error(f"步骤失败: {name}")
                   return False
   
           self.cleanup()
           self.logger.info("=== 部署完成 ===")
           return True
   
   # ==========================
   # 主函数
   # ==========================
   def main():
       parser = argparse.ArgumentParser(description="高级自动化部署脚本")
       parser.add_argument("--git-repo", required=True)
       parser.add_argument("--deploy-dir", required=True)
       parser.add_argument("--service-names", default="", help="多个服务用逗号分隔")
       parser.add_argument("--branch", default="main")
       args = parser.parse_args()
   
       config = DeploymentConfig(
           git_repo=args.git_repo,
           deploy_dir=Path(args.deploy_dir),
           service_names=[s.strip() for s in args.service_names.split(",") if s.strip()],
           branch=args.branch
       )
   
       deployer = Deployer(config)
       success = deployer.run()
       sys.exit(0 if success else 1)
   
   if __name__ == "__main__":
       main()
   
   ```

   





   