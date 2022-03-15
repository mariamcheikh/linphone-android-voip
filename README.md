# linphone-android-voip

### Les ajustements qui ont été nécessaires pour la compilation 

Veuillez trouver les modifications suivantes qui devaient être effectuées afin d'obtenir un résultat en cours d'exécution.


1) Ajouter FirebaseMessaging gradle  :

le service liblinphone FirebaseMessaging existe déjà dans l'application, comme indiqué dans le fichier AndroidManifest.xml
```
 <service android:name="org.linphone.core.tools.firebase.FirebaseMessaging"
            android:enabled="${firebaseServiceEnabled}"
            android:exported="false">
            <intent-filter>
                <action android:name="com.google.firebase.MESSAGING_EVENT" />
            </intent-filter>
        </service>   
 ```    

mais manquant la dépendance firebase dans le fichier gradle de notre application, nous avions donc besoin d'ajouter cette ligne :

```
classpath 'com.google.firebase:firebase-messaging:23.0.1'
```


2) Une erreur s'est produite avec l'URL manquante, j'ai donc ajouté :
``` 
tools:ignore="AppLinkUrlError" ajoutez aussi  xmlns:tools="http://schemas.android.com/tools" s'il n'y est pas déjà.
```

### Résultats

(Veuillez trouver les captures d'écran de l'application en cours d'exécution dans le dossier "results") :


### L'architecture générale d'une application voip :
( ce diagrame 
![architecture](https://user-images.githubusercontent.com/25226887/158408031-2fceac87-0b06-42ad-9041-a83c669b947f.jpg)


### L'architecture générale Linphone:
d'après [https://www.linphone.org/technical-corner/linphone](url) <br /> 
![Capture](https://user-images.githubusercontent.com/25226887/158457942-b7304afd-6933-4073-a903-54e92984639d.PNG) <br /> 
Plus de détails:  <br />  
![architecture linphone](https://user-images.githubusercontent.com/25226887/158412628-f276e407-81eb-4c64-b4a9-8c164f43c662.jpg) <br /> 

#### Explication détaillé:  <br /> 

Cette l'implémentation logicielle peut être utilisée pour communiquer librement avec des personnes sur Internet, avec la messagerie instantanée vocale, vidéo et textuelle.<br /> Linphone utilise le protocole SIP, un standard ouvert pour la téléphonie Internet, pour la communication . Et il est disponible pour ordinateurs de bureau exécutant Linux, Windows et MacOSX ou des smartphones fonctionnant sous Android et iOS. <br />  Dans cette cas nous intéressons sur L'application Android. <br />
Puisque Linphone peut adopter différents mécanismes de codec et prendre en charge divers systèmes d'exploitation, nous utilisons Linphone sur des systèmes intégrés pour mettre en œuvre le service de diffusion VoIP.<br />
Il y a deux parties principales dans Linphone :<br />  l'une est l'utilisateur interface et l'autre est le moteur de base.<br /> GTK+/clairière est utilisé pour l'interface graphique et une application en mode console. <br /> 
* Le moteur de base est Liblinphone qui est la bibliothèque implémentant toutes les fonctionnalités de Linphone.<br />

Liblinphone est un puissant SDK vidéo SIP VoIP qui peut être utilisé pour ajouter des capacités d'appel audio ou vidéo à une applicationet fournit une API de haut niveau pour initier, recevoir ou terminer appels. <br /> La communication multimédia est généralement faite de riches médias (tels que la voix ou la vidéo) et la signalisation (telle que les appels et prise d'appel). Linphone vise à rejoindre ces deux choses pour implémenter les appels vocaux/vidéo dans les applications facilement.

 Liblinphone dépend de trois composants logiciels — (1) Mediastreamer2, (2) oRTP et (3) eXosip2.
* (1) Mediastreamer2 : une bibliothèque qui se charge de recevoir et envoyer des flux multimédias dans Linphone, y compris la capture vocale/vidéo, l'encodage et décodag. Bref, c'est un puissant moteur de streaming léger spécialisé dans les applications de téléphonie vocale/vidéo.
* (2) oRTP : une bibliothèque de protocoles de transport en temps réel qui inclut des API pour analyser les paquets RTCP entrants. ça prend en charge plusieurs profils et l'AV (audio/vidéo) le profil est celui par défaut. Il peut également prendre en charge le SRTP (RTP sécurisé).
* (3) eXosip : une librairie qui cache la complexité d'utiliser  le protocole SIP pour la construction de sessions multimédia.


