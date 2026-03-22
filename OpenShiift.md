
## 1. Что такое OpenShift и чем он отличается от Kubernetes?

**Ответ:**  
OpenShift — это корпоративная Kubernetes-платформа от Red Hat. Помимо “чистого” Kubernetes, он добавляет:

- встроенную безопасность (SCC, SELinux),
    
- CI/CD (Pipelines, Builds),
    
- встроенный registry,
    
- web-консоль,
    
- строгую модель RBAC и multitenancy.
    

---

## 2. Какие основные компоненты OpenShift-кластера?

**Ответ:**

- Control Plane (API Server, Scheduler, Controller Manager, etcd)
    
- Worker-ноды
    
- Ingress Controller (Routes)
    
- Image Registry
    
- Operators
    
- Authentication и RBAC
    

---

## 3. Что такое Project в OpenShift и чем он отличается от Namespace?

**Ответ:**  
Project — это расширенный Namespace.  
Он включает:

- Namespace,
    
- RBAC,
    
- ResourceQuota,
    
- LimitRange,
    
- аннотации и метаданные.  
    Проект — базовая единица multitenancy в OpenShift.
    

---

## 4. Что такое Route и чем она отличается от Ingress?

**Ответ:**  
Route — это OpenShift-специфичный объект для публикации сервиса наружу.  
В отличие от Ingress:

- проще в настройке,
    
- нативно поддерживает TLS (edge, passthrough, re-encrypt),
    
- интегрирован с OpenShift Router.
    

---

## 5. Какие типы TLS есть у Route?

**Ответ:**

- **Edge** — TLS завершается на роутере
    
- **Passthrough** — TLS идёт напрямую в pod
    
- **Re-encrypt** — TLS до роутера и заново до pod
    

---

## 6. Что такое Security Context Constraints (SCC)?

**Ответ:**  
SCC — это механизм безопасности, определяющий:

- под каким UID запускается контейнер,
    
- можно ли использовать privileged,
    
- доступ к hostPath, capabilities, SELinux.  
    В OpenShift pod **по умолчанию не может запускаться как root**.
    

---

## 7. Почемуонтейнеры в OpenShift не запускаютсяпод root?

**Ответ:**  
Это требование безопасности.  
OpenShift использует random UID и SELinux, чтобы:

- изолировать приложения,
    
- снизить риск эскалации привилегий,
    
- соответствовать enterprise security стандартам.
    


## 8. Что такое Operator в OpenShift?

**Ответ:**  
Operator — это контроллер, который автоматизирует:

- установку,
    
- обновление,
    
- масштабирование,
    
- backup и recovery приложений.  
    По сути — “DevOps в коде”.
    

---

## 9. Что такое Operator Lifecycle Manager (OLM)?

**Ответ:**  
OLM управляет:

- установкой Operators,
    
- версиями,
    
- каналами обновлений,
    
- зависимостями.  
    Позволяет безопасно обновлять Operators в кластере.
    

---

## 10. Как работает аутентификация в OpenShift?

**Ответ:**  
OpenShift поддерживает:

- OAuth,
    
- LDAP,
    
- GitHub / GitLab,
    
- OpenID Connect.  
    Аутентификация централизована через OAuth-сервер.
    

---

## 11. Как реализован RBAC в OpenShift?

**Ответ:**  
RBAC основан на Kubernetes, но:

- роли привязываются к Project,
    
- есть cluster-roles,
    
- есть дополнительные роли OpenShift (admin, edit, view).
    

---

## 12. Что такое BuildConfig?

**Ответ:**  
BuildConfig описывает процесс сборки образа:

- Source-to-Image (S2I),
    
- Docker build,
    
- Jenkins pipeline.  
    Это нативный CI-механизм OpenShift.
    

---

## 13. Что такое Source-to-Image (S2I)?

**Ответ:**  
S2I — это механизм сборки образов из исходного кода без Dockerfile.  
Он берёт:

- исходники,
    
- builder-image,
    
- и собирает runnable image автоматически.
    

---

## 14. Как работает Image Registry в OpenShift?

**Ответ:**  
Встроенный registry:

- хранит образы внутри кластера,
    
- интегрирован с RBAC,
    
- поддерживает image streams,
    
- может использовать внешнее хранилище (S3, NFS).
    

---

## 15. Что такое ImageStream?

**Ответ:**  
ImageStream — это абстракция над docker-image:

- хранит версии тегов,
    
- позволяет делать автоматические redeploy при обновлении образа,
    
- упрощает CI/CD.
    

---

## 16. Как происходит деплой приложения в OpenShift?

**Ответ:**  
Типовой флоу:

1. Build image (BuildConfig / Pipeline)
    
2. ImageStream обновляется
    
3. DeploymentConfig / Deployment триггерит rollout
    
4. Route публикует сервис
    

---

## 17. Чем DeploymentConfig отличается от Deployment?

**Ответ:**  
DeploymentConfig — OpenShift-специфичный:

- поддерживает image change triggers,
    
- legacy механизм.  
    Deployment — стандарт Kubernetes, сейчас рекомендуется именно он.
    

---

## 18. Как мониторинг реализован в OpenShift?

**Ответ:**  
Используется:

- Prometheus,
    
- Alertmanager,
    
- Grafana.  
    Мониторятся:
    
- кластер,
    
- ноды,
    
- pods,
    
- приложения.
    

---

## 19. Как логирование реализовано в OpenShift?

**Ответ:**  
Используется EFK/LOKI стек:

- Fluentd / Vector,
    
- Elasticsearch / Loki,
    
- Kibana / Grafana.  
    Логи централизованы и привязаны к namespace.
    

---

## 20. Какие типичные проблемы при работе с OpenShift?

**Ответ:**

- Падения pod из-за SCC
    
- Проблемы с правами (RBAC)
    
- Ошибки Route/TLS
    
- Нехватка ресурсов (Quota, LimitRange)
    
- SELinux/FS permissions
    
