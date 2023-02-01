
# Brief 6: executive summary

---

## Objectifs

----

- utiliser kubernetes et aks
- déployer application de vote
- BDD redis
- stockage persistant pour la BDD
- zone DNS
- application gateway via ingress

----

<section data-visibility="hidden">
## installation de kubctl

- sudo `apt-get install -y kubect`
- création d'un groupe de ressource azure (dans mon cas "gabriel_brief6")
- création d'un cluster aks (dans mon cas "kuber") `az aks create -g gabriel_brief6 -n kuber --ssh-key-value /chemin/de/la/clé --node-count 4 --enable-managed-identity -a ingress-appgw --appgw-name myApplicationGateway --appgw-subnet-cidr "10.225.0.0/16"`
- connexion de kubectl et aks `az aks get-credentials --resource-group gabriel_brief6 --name kuber`
</section>

---


## création du certificat SSL

via OVH et certbot
cercificat -> K8s secrets -> ingress
[rajaxpression.distributeur-de-pain.best](https://rajaxpression.distributeur-de-pain.best/)

---

## ressources azure
- azure kubernetes service
    - 2 nodes
    - ingress application gateway

---

## création des templates k8s

----

- Secrets
    - mot de passe pour redis
    - certificat TLS
    - clé privée TLS
- storage
    - storageclass
    - PersistentVolumeClaim
- redis
    - deployment redis
    - clusterIP redis
- ingress
    - ingress azure application gateway
- voting app
    - deployment voteapp
    - clusterIP voteapp
    - HorizontalPodAutoscaler

---

## déploiement du cluster

- `kubectl apply -f chemin/du/dossier`

---

## test de charge
Horizontal pod autoscaler
permet en réponse à une monté en charge des pods présents d'en déployer jusqu'à 8.

---

## explication k8s

- open-source
- orchestration de conteneurs
- configuration déclarative
- gestion d'applications à grandes échelles
- déploiement de pods et de services sur des nodes
- yaml/Json -> contrôleur -> nodes
