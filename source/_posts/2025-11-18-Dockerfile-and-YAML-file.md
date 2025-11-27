---
title: Dockerfile and YAML file 
date: 2025-11-18
tag: 练习
categories: 容器
---

# Dockerfile与YAML文件编写练习

## Dockerfile编写练习

1. ### 基础Nginx镜像

   ```dockerfile
   # 基于官方Nginx镜像，添加自定义HTML页面
   FROM nginx:alpine
   COPY index.html /usr/share/nginx/html/
   EXPOSE 80
   ```

2. ### Python Flask应用

   ```dockerfile
   # 构建Python Flask应用镜像
   FROM python:3.9-slim
   WORKDIR /app
   COPY requirements.txt .
   RUN pip install -r requirements.txt
   COPY . .
   EXPOSE 5000
   CMD ["python", "app.py"]
   ```

3. ### 多阶段构建Node.js应用

   ```dockerfile
   # 构建阶段
   FROM node:16 AS builder
   WORKDIR /app
   COPY package*.json ./
   RUN npm ci
   COPY . .
   RUN npm run build
   
   # 生产阶段
   FROM nginx:alpine
   COPY --from=builder /app/dist /usr/share/nginx/html
   EXPOSE 80
   ```

4. ### 带健康检查的数据库

   ```dockerfile
   FROM postgres:13
   COPY init.sql /docker-entrypoint-initdb.d/
   HEALTHCHECK --interval=30s --timeout=3s \
     CMD pg_isready -U postgres || exit 1
   ```

5. ### 自定义用户运行应用

   ```dockerfile
   FROM node:16-alpine
   RUN addgroup -g 1001 -S appgroup && \
       adduser -S appuser -u 1001
   WORKDIR /app
   COPY --chown=appuser:appgroup . .
   USER appuser
   CMD ["node", "server.js"]
   ```

6. ### 优化缓存的Python应用

   ```dockerfile
   FROM python:3.9-slim
   WORKDIR /app
   # 先复制依赖文件，利用Docker缓存
   COPY requirements.txt .
   RUN pip install --no-cache-dir -r requirements.txt
   # 再复制源代码
   COPY . .
   CMD ["gunicorn", "-w", "4", "app:app"]
   ```

7. ### 多架构构建准备

   ```dockerfile
   # 使用显式架构标签
   FROM --platform=$BUILDPLATFORM node:16 AS builder
   WORKDIR /app
   COPY package.json .
   RUN npm install
   COPY . .
   RUN npm run build
   
   FROM nginx:alpine
   COPY --from=builder /app/dist /usr/share/nginx/html
   ```

8. ### 带环境变量的应用

   ```dockerfile
   FROM python:3.9
   WORKDIR /app
   COPY . .
   ENV FLASK_ENV=production \
       DATABASE_URL=postgresql://user:pass@db:5432/app
   RUN pip install -r requirements.txt
   EXPOSE 8000
   CMD ["gunicorn", "app:app", "-b", "0.0.0.0:8000"]
   ```

9. ### 使用Build Args

   ```dockerfile
   FROM ubuntu:20.04
   ARG DEBIAN_FRONTEND=noninteractive
   ARG APP_VERSION=1.0.0
   RUN apt-get update && apt-get install -y nginx
   COPY nginx.conf /etc/nginx/nginx.conf
   LABEL version=$APP_VERSION
   EXPOSE 80
   CMD ["nginx", "-g", "daemon off;"]
   ```

10. ### 复杂应用依赖

    ```dockerfile
    FROM ubuntu:20.04
    RUN apt-get update && apt-get install -y \
        python3 \
        python3-pip \
        curl \
        git \
        && rm -rf /var/lib/apt/lists/*
    WORKDIR /app
    COPY requirements.txt .
    RUN pip3 install -r requirements.txt
    COPY . .
    RUN chmod +x startup.sh
    CMD ["./startup.sh"]
    ```

## YAML 文件编写练习

1. ### 基础Pod配置

   ```yaml
   apiVersion: v1
   kind: Pod
   metadata:
     name: web-pod
     labels:
       app: web
       environment: production
   spec:
     containers:
     - name: nginx
       image: nginx:1.21
       ports:
       - containerPort: 80
       resources:
         requests:
           memory: "128Mi"
           cpu: "100m"
         limits:
           memory: "256Mi"
           cpu: "200m"
   ```

2. ### Deployment配置

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: api-deployment
   spec:
     replicas: 3
     selector:
       matchLabels:
         app: api
     template:
       metadata:
         labels:
           app: api
       spec:
         containers:
         - name: api
           image: myapp/api:1.0.0
           ports:
           - containerPort: 8080
           env:
           - name: DATABASE_URL
             valueFrom:
               secretKeyRef:
                 name: db-secret
                 key: connection-string
   ```

3. ### Service配置

   ```yaml
   apiVersion: v1
   kind: Service
   metadata:
     name: web-service
   spec:
     selector:
       app: web
     ports:
     - name: http
       port: 80
       targetPort: 80
       protocol: TCP
     type: LoadBalancer
   ```

4. ### ConfigMap配置

   ```yaml
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: app-config
   data:
     app.properties: |
       server.port=8080
       logging.level=INFO
       cache.enabled=true
     database.conf: |
       host=localhost
       port=5432
       pool.size=10
   ```

5. ### Secret配置

   ```yaml
   apiVersion: v1
   kind: Secret
   metadata:
     name: database-secret
   type: Opaque
   data:
     username: YWRtaW4=
     password: cGFzc3dvcmQxMjM=
     connection-string: cG9zdGdyZXNxbDovL3VzZXI6cGFzc0BkYjU0MzIxLmNvbQ==
   ```

6. ### 有状态应用StatefulSet

   ```yaml
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: database
   spec:
     serviceName: "database"
     replicas: 3
     selector:
       matchLabels:
         app: database
     template:
       metadata:
         labels:
           app: database
       spec:
         containers:
         - name: postgres
           image: postgres:13
           ports:
           - containerPort: 5432
           env:
           - name: POSTGRES_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: db-secret
                 key: password
           volumeMounts:
           - name: data
             mountPath: /var/lib/postgresql/data
     volumeClaimTemplates:
     - metadata:
         name: data
       spec:
         accessModes: [ "ReadWriteOnce" ]
         resources:
           requests:
             storage: 10Gi
   ```

7. ### 水平Pod自动扩缩容

   ```yaml
   apiVersion: autoscaling/v2
   kind: HorizontalPodAutoscaler
   metadata:
     name: web-hpa
   spec:
     scaleTargetRef:
       apiVersion: apps/v1
       kind: Deployment
       name: web-deployment
     minReplicas: 2
     maxReplicas: 10
     metrics:
     - type: Resource
       resource:
         name: cpu
         target:
           type: Utilization
           averageUtilization: 70
   ```

8. ### Ingress配置

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: Ingress
   metadata:
     name: app-ingress
     annotations:
       nginx.ingress.kubernetes.io/rewrite-target: /
   spec:
     rules:
     - host: myapp.example.com
       http:
         paths:
         - path: /
           pathType: Prefix
           backend:
             service:
               name: web-service
               port:
                 number: 80
     - host: api.example.com
       http:
         paths:
         - path: /api
           pathType: Prefix
           backend:
             service:
               name: api-service
               port:
                 number: 8080
   ```

9. ### 网络策略

   ```yaml
   apiVersion: networking.k8s.io/v1
   kind: NetworkPolicy
   metadata:
     name: api-network-policy
   spec:
     podSelector:
       matchLabels:
         app: api
     policyTypes:
     - Ingress
     - Egress
     ingress:
     - from:
       - podSelector:
           matchLabels:
             app: web
       ports:
       - protocol: TCP
         port: 8080
     egress:
     - to:
       - podSelector:
           matchLabels:
             app: database
       ports:
       - protocol: TCP
         port: 5432
   ```

10. ### 完整的应用部署

    ```yaml
    # 多资源文件，包含Deployment、Service、ConfigMap
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: frontend-config
    data:
      config.js: |
        window.APP_CONFIG = {
          apiUrl: "/api/v1",
          environment: "production"
        }
    ---
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: frontend-deployment
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: frontend
      template:
        metadata:
          labels:
            app: frontend
        spec:
          containers:
          - name: nginx
            image: nginx:alpine
            ports:
            - containerPort: 80
            volumeMounts:
            - name: config
              mountPath: /usr/share/nginx/html/config.js
              subPath: config.js
          volumes:
          - name: config
            configMap:
              name: frontend-config
    ---
    apiVersion: v1
    kind: Service
    metadata:
      name: frontend-service
    spec:
      selector:
        app: frontend
      ports:
      - port: 80
        targetPort: 80
      type: ClusterIP
    ```

