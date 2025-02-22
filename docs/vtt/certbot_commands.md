# Génération de certificats pour Foundry VTT

Ces notes sont basées sur [Raspberry Pi SSL Certificates using Let’s Encrypt](https://pimylifeup.com/raspberry-pi-ssl-lets-encrypt/) et sur la documentation [SSL and HTTPS](https://foundryvtt.com/article/ssl/) de Foundry. Elles résument et rappellent les commandes pour obtenir des certificats [Let’s Encrypt](https://letsencrypt.org/) sur un Raspberry Pi afin de les utiliser avec [Foundry VTT](https://foundryv.tt.com/).


## Installation de [Certbot](https://certbot.eff.org/)
```
sudo apt install certbot
```

## Génération des certificats

Pour cette étape, dans la configuration de sa box Internet, il faut préalablement rediriger les ports 80 et 443 vers son Raspberry Pi.

```bash
export DOMAIN_NAME=vtt.ludorg.net
sudo certbot certonly --standalone -d ${DOMAIN_NAME}
```

Les certificats sont dans `/etc/letsencrypt/live/${DOMAIN_NAME}`. Ce sont des liens symboliques vers les fichiers dans `/etc/letsencrypt/live/${DOMAIN_NAME}/../../archive/${DOMAIN_NAME}/`.

Pour Foundry VTT, il faut récupérer les fichiers `fullchain.pem` et `privkey.pem` et les copier dans le dossier `Config`.

Ces certificats sont valides 90 jours. Il ne faut donc pas oublier de les renouveler.