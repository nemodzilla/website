---
title: "Git — Commandes utiles"
description: "Rappels des commandes Git pour mettre à jour le site"
date: 2026-03-12
slug: "git-cheatsheet"
categories:
    - Astuces
tags:
    - git
draft: false
---

## Mettre à jour le site
```bash
git add .
git commit -m "Description de ce que j'ai changé"
git push
```

## Enlever des fichiers déjà ajoutés au staging

Si j'ai fait un `git add` mais que je veux annuler avant de commiter :
```bash
# Enlever un fichier spécifique du staging
git reset HEAD nom-du-fichier

# Enlever tous les fichiers du staging
git reset HEAD .
```

> ⚠️ Les modifications ne sont pas perdues, elles sont juste "déstagées".

## Voir ce qui est staged
```bash
git status
```

## Workflow complet pour mettre à jour le site
```bash
# 1. Voir ce qui a changé
git status

# 2. Ajouter les modifications
git add .

# 3. Commiter avec un message clair
git commit -m "Add writeup: nom-du-challenge"

# 4. Pousser → le site se met à jour automatiquement en ~1 minute
git push
```

## Annuler le dernier commit (sans perdre les modifications)
```bash
git reset --soft HEAD~1
```

## Rétablir une ancienne version

# 1. Pour avoir le hash de la version
```bash
git log --oneline
```

# 2. Restaurer

```bash
git revert --no-commit XXXXXXX..HEAD
git commit -m "Revert to vXX"
git push
```