---
title: Homemade Keylogger
description: RootMe - Homemade Keylogger
slug: RMHomemadeKeylogger
date: 2024-03-03 00:00:00+0000
image : assets/forensic.jpg
categories:
    - RootMe
tags:
    - Forensic
---

[Link to the challenge](https://www.root-me.org/en/Challenges/Forensic/Homemade-keylogger)

## Solution
{{< flag "3ddbc1fb4fb9bb0af6c95d6fc3ac64c49c70caddf39c417c088a970e1a9846ee" "1" >}}


```python
import base64

# Lire le contenu du fichier ch24.txt
with open('ch24.txt', 'r') as f:
    base64_encoded = f.read()

# Déchiffrer le contenu base64
decoded_bytes = base64.b64decode(base64_encoded)

# Écrire le contenu déchiffré dans un autre fichier
with open('ch24_decoded.txt', 'wb') as f:
    f.write(decoded_bytes)
```

```binary
 0
Z    
           0
Z    
            0
Z    
              0
Z            8    0
Z           8     0
Z                   0
Z     `       8    0
Z     `      8     0
Z     `              0
Z    F        8    0
Z    F       8     0
Z    F               0
Z    U       8    0
Z    U      8     0
Z    U              0
Z             8    0
Z            8     0
Z                    0
Z    `Q       8    0
Z    `Q      8     0
Z    `Q              0
Z    b        8    0
Z    b       8     0
Z    b               0
Z    ,V       8    0
Z    ,V      8     0
Z    ,V              0
Z    p        8    0
Z    p       8     0
Z    p               0
Z    ]I       8    0
Z    ]I      8     0
Z    ]I              0
Z    V        8    0
Z    V       8     0
Z    V               0
Z    <       8    0
Z    <      8     0
Z    <              0
Z    f        8    0
Z    f       8     0
Z    f               0
Z    6        8    0
Z    6       8     0
Z    6               0
Z    ,         8    0
Z    ,        8     0
Z    ,                0
Z     *       8    0
Z     *      8     0
Z     *              0
Z            8    0
Z           8     0
Z                   0
Z     %	       8    0
Z     %	      8     0
Z     %	              0
Z    j 	       8    0
Z    j 	      8     0
Z    j 	              0
Z    8,
       8    0
Z    8,
      8     0
Z    8,
```

```python
import struct

# Ouvrir le fichier ch24_decrypted.txt
f= open('ch24_decoded.txt', 'rb');
f_out = open('decoded.txt', 'w')

while 1:
    data = f.read(24)
    if not data:
        break
    f_out.write(str(struct.unpack('4IHHI', data)) + '\n')

f.close()
f_out.close()
```

```txt
(1510682841, 0, 726788, 0, 4, 4, 28)
(1510682841, 0, 726788, 0, 1, 28, 0)
(1510682841, 0, 726788, 0, 0, 0, 0)
(1510682842, 0, 842767, 0, 4, 4, 56)
(1510682842, 0, 842767, 0, 1, 56, 1)
```

```python
# Ouvrir le fichier en mode lecture
with open('decoded.txt', 'r') as file:
    # Créer un nouveau fichier pour écrire
    with open('resultat.txt', 'w') as resultat_file:
        # Lire chaque ligne du fichier
        for line in file:
            # Supprimer les parenthèses et les virgules et diviser la ligne en une liste
            elements = line.strip('()').split(',')

            # Récupérer l'avant-dernier élément de la liste et le stocker dans un tableau
            avant_dernier = elements[-2]

            # Écrire l'avant-dernier élément dans le fichier résultat
            resultat_file.write(avant_dernier + '\n')
```

```python
# Ouvrir le fichier d'entrée en mode lecture
with open('decoded.txt', 'r') as file:
    # Ouvrir le fichier de résultat en mode écriture
    with open('resultat.txt', 'w') as result_file:
        # Parcourir chaque ligne du fichier d'entrée
        for line in file:
            # Supprimer les parenthèses et les espaces
            line = line.strip('() \n')
            # Séparer les champs en une liste
            fields = line.split(', ')
            # Vérifier si les champs 4 et 6 sont égaux à 1
            if fields[4] == '1' and fields[6] == '1':
                # Écrire la valeur du champ 5 dans le fichier de résultat
                result_file.write(fields[5] + '\n')
```

> javier_turcot

{{< /flag >}}
