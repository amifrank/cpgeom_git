# Découverte de GIT

![LOGO GIT](/image/Git-logo.svg.png "Logo GIT")

Prise en main de GIT

## Démonstration  

> Création d'un repo local

```bash
mkdir 00-git-local &&
cd 00-git-local
```

> Édition de ce fichier README.md, en guise de page d'acceuil de mon futur repo

```bash
touch README.md
nano README.md
```

---

## Push via SSH

### 1. Configurer son identité Git (une seule fois)

```bash
git config --global user.name "Ton Nom"
git config --global user.email "ton.email@example.com"
```

### 2. Générer une clé SSH (une seule fois)

```bash
ssh-keygen -t ed25519 -C "ton.email@example.com"
```

> Valider avec Entrée pour garder le chemin par défaut (`~/.ssh/id_ed25519`).

### 3. Démarrer l'agent SSH et charger la clé

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### 4. Copier la clé publique

```bash
cat ~/.ssh/id_ed25519.pub
```

> Copier tout le contenu affiché (commence par `ssh-ed25519 ...`).

### 5. Ajouter la clé publique dans GitHub

1. Aller dans **GitHub > Settings > SSH and GPG keys**
2. Cliquer sur **New SSH key**
3. Coller la clé publique
4. Sauvegarder

### 6. Tester la connexion SSH

```bash
ssh -T git@github.com
```

> Répondre `yes` si demandé. Résultat attendu :
> `Hi <username>! You've successfully authenticated...`

### 7. Initialiser le repo local

```bash
git init
```

### 8. Relier le repo local au repo GitHub en SSH

```bash
git remote add origin git@github.com:TON_USER/NOM_DU_REPO.git
```

> Si `origin` existe déjà :
> ```bash
> git remote set-url origin git@github.com:TON_USER/NOM_DU_REPO.git
> ```

Vérifier le remote :

```bash
git remote -v
```

### 9. Premier commit et push

```bash
git add .
git commit -m "Premier commit"
git branch -M main
git push -u origin main
```

### 10. Workflow quotidien

```bash
git add .
git commit -m "Message de commit"
git push
```

---

## Dépannage

| Problème | Solution |
|---|---|
| `Permission denied (publickey)` | Vérifier avec `ssh-add -l`, recharger la clé avec `ssh-add ~/.ssh/id_ed25519` |
| Push en HTTPS au lieu de SSH | `git remote set-url origin git@github.com:USER/REPO.git` |
| Mauvaise branche | `git branch` pour lister, puis `git push -u origin nom_branche` |
