ArgoCD && Rollout
-----------------
    helm repo add argo https://argoproj.github.io/argo-helm
    helm repo update
    helm upgrade --install argocd argo/argo-cd -n argocd --create-namespace --version 9.5.11 --wait -f stack/argo/argocd-values.yaml
    helm upgrade --install argo-rollouts argo/argo-rollouts -n argo-rollouts --create-namespace --version 2.40.9 --wait -f stack/argocd/argo-rollouts-values.yaml

    argocd:
    -------
        user: admin
        pass: kc -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

        kc -n argocd port-forward service/argocd-server 8080:443

    argo-rollout:
    -------------
        karr port-forward service/argo-rollouts-dashboard 31000:3100

# Comentarios:

El plugin gatewayAPI de Argo Rollouts se usa porque Argo Rollouts necesita una forma de controlar el tráfico durante despliegues canary o blue/green, y en tu caso estás usando la especificación estándar Kubernetes SIG Network Gateway API junto con Istio Ambient Mesh. Este plugin permite que Rollouts modifique dinámicamente los pesos (weight) de los backendRefs dentro de los recursos HTTPRoute, logrando distribuir tráfico entre la versión estable y la canary (por ejemplo 90/10, 50/50, etc.) sin depender de APIs propietarias como VirtualService de Istio.

_________
# Imagenes:
edgarrth/demo-shippingservice:1.0.0
edgarrth/demo-cartservice:1.0.0
edgarrth/demo-checkoutservice:1.0.0
edgarrth/demo-productcatalogservice:1.0.0
edgarrth/frontend:main-95e15f4dd108
edgarrth/adservice:v0.10.5
edgarrth/loadgenerator:v0.10.5
edgarrth/emailservice:v0.10.5
edgarrth/currencyservice:v0.10.5
edgarrth/recommendationservice:v0.10.5
edgarrth/paymentservice:v0.10.5
edgarrth/redis:alpine