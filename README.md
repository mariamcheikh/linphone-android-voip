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

(Veuillez trouver les captures d'écran de l'application en cours d'exécution dans le dossier "results") :

