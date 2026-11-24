Étape 1 --- Créer et lancer le service

Question 1

Quelle annotation fait de EmpruntService un service web ? Quelle

annotation fait de LivreIndisponibleException une erreur déclarée dans

le contrat ?



Réponse :



L'annotation @WebService déclare la classe EmpruntService comme un

service web SOAP.



L'annotation @WebFault permet de déclarer LivreIndisponibleException

comme une exception métier associée au contrat du service. Elle permet à

JAX-WS de représenter cette exception dans le WSDL comme une Fault

déclarée.

Question 2

Pourquoi les classes de données doivent-elles avoir un constructeur

vide ?



Réponse :



Les classes de données doivent posséder un constructeur sans argument

afin que JAXB puisse créer les objets Java lors de la désérialisation

des messages XML en objets Java. Le constructeur vide facilite donc la

conversion entre XML et objets Java.

Étape 2 --- Lire le WSDL généré

Question 1

Quelle est l'URL du service ? Quelles sont les deux opérations et

leurs messages d'entrée et de sortie ?



Réponse :



L'URL du service est :



http://localhost:8080/bib/EmpruntService



Le service expose deux opérations :

1\. emprunterLivre

&#x20;  - Entrée : idAdherent et isbn.

&#x20;  - Sortie : un objet Emprunt, contenant numero et

&#x20;    dateRetour.

&#x20;  - Fault déclarée : LivreIndisponible.

2\. rendreLivre

&#x20;  - Entrée : numeroEmprunt.

&#x20;  - Sortie : penalite, de type Java BigDecimal.

Question 2

Quel style (document ou rpc) et quel use (literal ou encoded)

le binding déclare-t-il ? Est-ce du SOAP 1.1 ou 1.2 ?



Réponse :



Le binding utilise le style document et le mode literal.



Il s'agit de SOAP 1.1. Le namespace utilisé pour l'enveloppe SOAP 1.1

est :



http://schemas.xmlsoap.org/soap/envelope/

Question 3

Quel type XSD a été généré pour isbn et pour dateRetour ? La règle

de format de l'ISBN apparaît-elle ?



Réponse :



Dans le code Java du TP, isbn est un paramètre de type String et

dateRetour est un champ de type String. Ils sont donc normalement

représentés par le type XSD xs:string.



La règle de format de l'ISBN est définie dans le code Java à l'aide

d'une expression régulière (Pattern). Elle n'est pas automatiquement

traduite en restriction XSD dans cette approche code-first.

Question 4

Dans la requête SoapUI, les paramètres idAdherent et isbn

portent-ils un préfixe d'espace de noms ?



Réponse vérifiée à partir de la requête SoapUI fournie :



Non, les paramètres idAdherent et isbn ne portent pas de préfixe

explicite d'espace de noms dans la requête observée.



L'opération emprunterLivre porte le préfixe bib, associé au

namespace http://supnum.mr/bib. Les deux paramètres sont écrits sans

préfixe :

<bib:emprunterLivre>

&#x20;   <idAdherent>A-117</idAdherent>

&#x20;   <isbn>978-1-234-5678-9</isbn>

</bib:emprunterLivre>

Le préfixe soapenv est utilisé pour les éléments SOAP Envelope,

Header et Body.

Question 5

Dans l'onglet Raw, où voyez-vous HTTP, XML, SOAP ? Quel rôle joue

chacun de ces standards, et quel rôle joue le WSDL ?



Réponse :



Dans l'onglet Raw de SoapUI :

\- HTTP apparaît dans la ligne de requête, par exemple POST, et

&#x20; dans les en-têtes HTTP. Il assure le transport des messages entre le

&#x20; client et le serveur.

\- XML est le format textuel utilisé pour représenter les données

&#x20; échangées.

\- SOAP apparaît dans la structure de l'enveloppe, notamment

&#x20; Envelope, Header et Body. Il définit la structure des messages

&#x20; échangés.

\- WSDL décrit le contrat du service : son adresse, ses opérations,

&#x20; les messages d'entrée et de sortie ainsi que les types de données.

&#x20; Il permet à un outil comme SoapUI de comprendre le service et de

&#x20; générer les requêtes.

Récapitulatif des réponses

&#x20; Élément                             Réponse

&#x20; Annotation du service               @WebService



&#x20; Annotation de la Fault métier       @WebFault



&#x20; Constructeur vide                   Permet à JAXB de créer les objets pendant la

désérialisation XML



&#x20; URL du service                      http://localhost:8080/bib/EmpruntService



&#x20; Opérations                          emprunterLivre, rendreLivre



&#x20; Style du binding                    document



&#x20; Use du binding                      literal



&#x20; Version SOAP                        SOAP 1.1



&#x20; Type XSD de isbn                  xs:string



&#x20; Type XSD de dateRetour            xs:string



&#x20; Règle ISBN dans le XSD              Non, pas automatiquement dans cette approche

code-first



&#x20; Préfixe de idAdherent dans la     Aucun préfixe explicite

requête observée                    



&#x20; Préfixe de isbn dans la requête   Aucun préfixe explicite

observée                            



&#x20; HTTP                                Transport des messages



&#x20; XML                                 Représentation des données



&#x20; SOAP                                Structure des messages

WSDL                                Contrat descriptif du service

