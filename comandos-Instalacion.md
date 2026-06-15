# Gitea:
------

## Instalación y uso
    docker compose up -d gitea
    -> http://localhost:3000
    -> crear usuario (e.g. root/root123)
    -> clic > profile > site administratio > actions > Runners > Create new Runner > copy token

    docker compose --profile runner run --rm runner-register
    docker compose --profile runner up -d

    git init
    git branch -M main

    git add ...
    git commit -am ...

    git remote add origin http://localhost:3000/root/adservice.git
    git push -u origin main

    git remote add origin http://localhost:3000/root/adservice.git
    git push -u origin main

    git tags:
    ---------
    git tag -a v1.0.0 COMMIT_SHA -m "Release v1.0.0"

    git fetch origin main

    crear tag a partir de ultimo commit de rama remota
        git tag -a v1.0.0 origin/main -m "Release v1.0.0"

    crear tag a partir de ultimo commit de rama local
        git tag -a v1.0.0 main -m "Release v1.0.0"

    git push origin v1.0.0
    git push origin --tags
    git tag -d v1.0.0
    git push origin --delete v1.0.0

    git tag
    git show v1.0.0
    git ls-remote --tags origin

ArgoCD
------
    helm repo add argo https://argoproj.github.io/argo-helm
    helm repo update
    helm upgrade --install argocd argo/argo-cd -n argocd --create-namespace --version 9.5.11 --wait -f stack/argocd/argocd-values.yaml

    argocd:
    -------
        user: admin
        pass: kc -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

        kc -n argcd port-forward service/argocd-server 8080:443


# Instalacion CLIs Argos

## Argos CD CLI
instalar el CLI en Fedora WSL:

    curl -sSL -o argocd \
    https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64

    chmod +x argocd
    sudo mv argocd /usr/local/bin/

Luego:
    
    argocd version

Y para usarlo localmente:

    argocd login localhost:8080 --insecure

## Argos Rollout CLI
    
    curl -LO https://github.com/argoproj/argo-rollouts/releases/latest/download/kubectl-argo-rollouts-linux-amd64

    chmod +x kubectl-argo-rollouts-linux-amd64

    sudo mv kubectl-argo-rollouts-linux-amd64 /usr/local/bin/kubectl-argo-rollouts


 ______________________
 # Claves
 gitea: ZIOWh8FRSvtqnlonyUyEA80Yp6IsXuKGU97YngkP

