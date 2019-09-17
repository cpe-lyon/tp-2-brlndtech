# Compte rendu TP2  <img src="https://image.flaticon.com/icons/svg/518/518713.svg" height="50" alt="Zozor" /> | Geoffrey Sauvageot-Berland 

## Exercice 1 

### **1. Dans quels dossiers bash trouve-t-il les commandes tapées par l’utilisateur ?**

<code> printenv PATH </code>

### **2. Quelle variable d’environnement permet à la commande cd tapée sans argument de vous ramener dans votre répertoire personnel ?**

<code> printenv HOME</code> <br>
<code> /home/brlndtech </code> <br>

### **3. Explicitez le rôle des variables LANG, PWD, OLDPWD, SHELL et _.**

<code> printenv LANG  : fr_FR.UTF-8 </code> <br> 
<code> La variable d'environement LANG : La variable d'environnement « LANG » détermine la langue que les logiciels utilisent pour communiquer avec l'utilisateur </code> <br> <br>

<code> printenv PWD </code> <br>
<code> PWD : cette variable d'environement contient le chemin du répertoire courant. </code> <br> <br>

<code> printenv OLDPWD </code> <br>
<code> La variable d'envirronement $OLDPWD contient le chemin absolu vers le répertoire courant précédament visité </code><br>
<br>

<code> printenv SHELL : /bin/bash</code> <br>
<code> la variable d'environnement SHELL permet d'afficher le chemin du programme /bin/bash </code>


### **4. Créez une variable locale MY_VAR (le contenu n’a pas d’importance). Vérifiez que la variable existe**

<code> MY_VAR=" je suis une variable local"; </code> <br>
<code>
    echo $MY_VAR ; <br>
    "je suis une variable local" 
</code> <br>

### **5. Tapez ensuite la commande bash. Que fait-elle ? La variable MY_VAR existe-t-elle ? Expliquez. A la fin de cette question, tapez la commande exit pour revenir dans votre session initiale.**

<code> bash </code> <br>
<code> echo $MY_VAR (ne retourne rien) </code>

La variable MY_VAR n'éxiste plus, car elle à été "éffacée". La commande bash permet de relancer la consol du shell, et donc la variable local a été éliminé. 


### **6. Transformez MY_VAR en une variable d’environnement et recommencez la question précédente. Expliquez**

<code> export MY_VAR="coudcoud" <br> bash  <br> echo $MY_VAR ; <br> " coudcoud "</code> 

le fait d'utiliser export MY_VAR (...) ne crée pas une variable LOCAL, mais une variable GLOBAL. Elle reste donc dans le shell de manière permanente 

### **7.Créer la variable d’environnement NOMS ayant pour contenu vos noms de binômes séparés par un espace Afficher la valeur de NOMS pour vérifier que l’affectation est correcte**

<code> export NOMS="geoffrey bezet" <br> printenv NOMS </code>

### **8. Ecrivez une commande qui affiche ”Bonjour à vous deux, binôme1 binôme2 !” (où binôme1 et binôme2 sont vos deux noms) en utilisant la variable NOMS**

<code> echo "bonjour a vosu deux, $NOMS" </code> 

Pour rappel, NOM est une variable global édité juste avant 

### **9. Quelle différence y a-t-il entre donner une valeur vide à une variable et l’utilisation de la commande unset ?** 

<code> unset NOM <br> </code>
-> la variable qui a une valeur vide est toujours utilisable alors que grâce à la commande unset -> permet d'enlever la variable d'environnement NOM crée en amont. (On ne  pourrat plus l'afficher vu qu'elle n'éxiste plus )

### **10 Utilisez la commande echo pour écrire exactement la phrase : $HOME = chemin (où chemin est votre dossier personnel d’après bash)**

<code> echo "$HOME = chemin (où chemin est votre dossier personnel d’après bash)" </code> 

## Exercice 2 Programmation Bash

### **Vous enregistrerez vos scripts dans un dossier script que vous créerez dans votre répertoire personnel. Tous les scripts sont bien entendu à tester. Ajoutez le chemin vers script à votre PATH de manière permanente** 
```
cd ~  <br>
mkdir script  <br> 
cd script <br> 
touch testpasswd.sh <br>
nano testpasswd.sh <br>
chmod 700 testpasswd.sh <br>
<br>
```

```
#!/bin/bash <br>
PASSWORD_DB="coud"; <br>
passwordASaisir=""; <br>
read -p  "Saisissez votre mdp :  " -s passwordASaisir # -p  <br>
# -p pour afficher du texte "" -s = naffiche pas la saisie de user <br>
if [ $passwordASaisir = $PASSWORD_DB ]; then <br>
       echo -e "\n C'esttttttttt biiien ! password accepted :) " <br>
else <br>
        echo -e "\n wrong password" <br>
fi  <br>

```


## Exercice 3. Expressions rationnelles


```
#!/bin/bash

function is_number()
{
re='^[+-]?[0-9]+([.][0-9]+)?$'
if ! [[ $1 =~ $re ]] ; then
        return 1
else
        return 0
fi
}

is_number $1

if [ $? -eq 0 ]; then
        echo "Le nombre est de type réel (double)"
else
        echo "Le nombre n'est pas de type réel "
fi 
```
## Exercice 4. Contrôle d’utilisateur 
### Écrivez un script qui vérifie l’existence d’un utilisateur dont le nom est donné en paramètre du script. Si le script est appelé sans nom d’utilisateur, il affiche le message : ”Utilisation : nom_du_script nom_utilisateur”, où nom_du_script est le nom de votre script récupéré automatiquement (si vous changez le nom de votre script, le message doit changer automatiquement) 

```
#!/bin/bash
if [ -z "$1" ]; then
        echo "Utilisation : $0 user_name"
else
        if [ $(id -u $1) ]; then
                echo "the user exist !  "
        else
                echo "the user does not exist ! "
        fi
fi
```

## Exercice 5. Factoriel   


## Exercice 6. Le juste prix
```

#!/bin/sh
nombreAleatoire=$((1 + RANDOM % 10))
nombreASaisir="";
#echo $nombreAleatoire;
  read -p  "Saisissez un nombre entre 1 et 10 : "  nombreASaisir # -p
  while [  $nombreASaisir != $nombreAleatoire ]
  do                
      if [ $nombreASaisir > $nombreAleatoire ]; then  
            echo -e "\n Trop grand !! "
            read -p  "saisi à nouveau : "  nombreASaisir # -p affiche un
      elif [ $nombreASaisir < $nombreAleatoire ]; then
            echo -e "\nTrop petit !"
            read -p  "saisi à nouveau : "  nombreASaisir # -p affiche un
      fi
  done
echo "gagné !!! Le nombre était " $nombreAleatoire 
```
## Exercice 7. Statistiques
## Exercice 8. Pour les plus rapides






