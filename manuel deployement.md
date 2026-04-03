# 🔧 Étapes pour déployer le portfolio sur le serveur

## 1. Choisis le sous-domaine pour ton portfolio

Exemple : `portfolio.itachiyann.de` ou `cv.itachiyann.de` ou `projets.itachiyann.de`

## 2. Crée le dossier et le fichier

```bash
# Créer le dossier
sudo mkdir -p /var/www/portfolio.itachiyann.de/public_html

# Créer le fichier index.html
sudo vim /var/www/portfolio.itachiyann.de/public_html/index.html

3. Copie le code HTML ci-dessous dans le fichier

Colle-le dans Vim (i pour insérer, puis coller, puis :wq).
4. Applique les permissions et active le sous-domaine
bash

# Permissions
sudo chown -R www-data:www-data /var/www/portfolio.itachiyann.de/
sudo chmod -R 755 /var/www/portfolio.itachiyann.de/

# VirtualHost (HTTP)
sudo tee /etc/apache2/sites-available/portfolio.itachiyann.de.conf << 'EOF'
<VirtualHost *:80>
    ServerName portfolio.itachiyann.de
    DocumentRoot /var/www/portfolio.itachiyann.de/public_html
    <Directory /var/www/portfolio.itachiyann.de/public_html>
        Options -Indexes +FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/portfolio.itachiyann.de_error.log
    CustomLog ${APACHE_LOG_DIR}/portfolio.itachiyann.de_access.log combined
</VirtualHost>
EOF

# Activer le site
sudo a2ensite portfolio.itachiyann.de.conf
sudo systemctl reload apache2

# HTTPS avec Certbot
sudo certbot --apache -d portfolio.itachiyann.de

5. Teste

Ouvre ton navigateur et va sur : https://portfolio.itachiyann.de

Tu verras un portfolio moderne, avec cartes projets, badges, liens GitHub, et tout ton CV en version web.
text


---

Tu n'as plus qu'à copier-coller ce bloc dans ton terminal ou dans un fichier `.md` pour t'en souvenir. 🚀
