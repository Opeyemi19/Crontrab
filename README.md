# Django Crontab
Impletementation de Crontab dans Un project django

- cron est un programme qui permet aux utilisateurs des systèmes Unix ou MacOS d’exécuter automatiquement des scripts, des commandes ou des logiciels à une date et une heure spécifiée à l’avance, ou selon un cycle défini à l’avance.

-  Installation de django crontab ou a suivre sur https://pypi.org/project/django-crontab/

```python
  pip install django-crontab
```

- Ajout du package dans le Projet Django
```python

    INSTALLED_APPS = (
    'django_crontab',
    ...
)
```
- Ensuite Crée un ficher cron.py et cree le script ou la classe que l'on souhaite exceuter dans le fichier cron.py 

Exemple Nous allons excuter un script qui enregistre test dans la bd chaque trois minute
- dans notre cron.py on entre le code suvant:
```
  def nanus ():
    req = models.Nan(nom='test')
    req.save()
  
```

- Ensuite on ajout le script cree dans notre setting.py de l'application
```python
CRONJOBS = [
    ('*/3 * * * *', 'myapp.cron.nanus') # Ceci veut dire que a chaque 3minute la Fonction 'nanus' se trouvant dans le fichier **cron.py** cree dans l'application va s'executer.
]

Pour la gestion du Temps que l'on veut planifier on peut se referencer sur le site https://crontab.guru/#*_*_*_*_*

```

- Enfin, exécutez cette commande pour ajouter tous les travaux définis de CRONJOBS à crontab (de l'utilisateur avec lequel vous exécutez cette commande):
```python
python manage.py crontab add
```
- Apres avoir lancer le contrab vas generer un code
que l'on devra copier 
comme ceci:
```python
  adding cronjob: (964787d1407926910a1660d5aabdfa05) -> ('*/3 * * * *', 'myapp.cron.nanus')
```
- lancer cette commande pour le crontab 
```python
  python manage.py crontab run 964787d1407926910a1660d5aabdfa05
```
- NB: A chaque modification du fichier cron.py, on fait

```python
  python manage.py crontab run 964787d1407926910a1660d5aabdfa05
```
 * Si l'on modifie la duree d'execution alors on est oblige de supprimer le **cronjob** ajout au par avant a notre Path(Variable d' environnement: bash ou du Vim) 

```python
  python manage.py crontab remove
```

- Ensuite la commande add et lancer le run avec le code generer grace au **Time** que l'on a donne

