# BAPI

Une BAPI (Business Application Programming Interface) est une interface standardisée de SAP permettant d'accéder aux fonctionnalités des modules SAP via des programmes externes.

## Objectif : Utiliser la BAPI => "BAPI_SALESORDER_CREATEFROMDAT2"

### Documentation officielle :

```text
Functionality
You can use this method to create sales orders.

You must enter at least sales order header data (via ORDER_HEADER_IN structure) and partner data (via the ORDER_PARTNERS table) as input parameters.

Enter the item data via the ORDER_ITEMS_IN table. You can allocate item numbers manually, by filling in the relevant fields, or the system does it, according to the settings for Customizing, by leaving the relevant fields blank.

If you have configurable items, you must enter the configuration data in the ORDER_CFGS_REF, ORDER_CFGS_INST, ORDER_CFGS_PART_OF and ORDER_CFGS_VALUE tables.

Credit cards can be transferred via the BAPICCARD structure, on the one hand, data for card identification, on the other, data for a transaction which has taken place in an external system.

Once you have created the sales order successfully, you will receive the document number (SALESDOCUMENT field). Any errors that may occur will be announced via the RETURN parameter.

If no sales area has been created in the sales order header, then the system creates the sales area from the sold-to party or ship-to party, who has been entered in the partner table. If a clear sales area cannot be created, you will receive a system message, and the sales order will not be created.

PayPal Transactions

Two-step transactions with PayPal can also be transferred via BAPICARD structure. The two-step transaction with PayPal is similar to the payment with credit card. Therefore, the following settings are also used for payments with PayPal: Card category 01 for credit cards and payment plan type 03 for processing payment cards.

The following applies for payments with PayPal:

Use card type DP2P (field CC_TYPE)
Use service provider DPPP (field DP_PSP)
Transfer the complete authorization data
The following checks are made for PayPal transactions:

If card type equals DP2P (one-step transaction DP1P is currently not supported)
If no token is provided for DP2P cards
If an authorization ID is available
If only one PayPal payment is assigned
Concerning the "Limit to" functionality:
If the value to be billed (field BILLAMOUNT) is not transferred, the value is automatically set to the authorized amount (field AUTHAMOUNT).
If the value to be billed is transferred, it must be equal to the authorized amount; otherwise an error message occurs.
Notes
Mandatory entries:
ORDER_HEADER_IN : DOC_TYPE Sales document type
SALES_ORG Sales organization
DISTR_CHAN Distribution channel
DIVISION Division

ORDER_PARTNERS..: PARTN_ROLE Partner role, SP sold-to party
PARTN_NUMB Customer number

ORDER_ITEMS_IN..: MATERIAL Material number

Ship-to party:

If no ship-to party is entered, use the following: Ship-to party =
sold-to party.
Commit control:
The BAPI does not have a database commit. This means that the relevant application must leave the commit, in order that can be carried out on on the database. The BAPI BAPI_TRANSACTION_COMMIT is available for this.
German key words:
The following key words must be entered in German, independantly of
the logon language:
DOC_TYPE Sales document type, for example: TA for standard order
PARTN_ROLE Partner role, for example: WE for ship-to party
Further Information
You can find further information in the OSS. The note 93091 contains general information on the BAPIs in SD.
```

### Résumé des points importants de la BAPI "BAPI_SALESORDER_CREATEFROMDAT2"

- **Fonction principale** : Créer des commandes clients dans SAP.
- **Paramètres obligatoires** :
  - **ORDER_HEADER_IN** : DOC_TYPE (type de document de vente), SALES_ORG (organisation commerciale), DISTR_CHAN (canal de distribution), DIVISION (division).
  - **ORDER_PARTNERS** : PARTN_ROLE (rôle partenaire, SP pour le client principal), PARTN_NUMB (numéro de client).
  - **ORDER_ITEMS_IN** : MATERIAL (numéro de matériau).
- **Attribution des numéros d'articles** : Manuelle ou automatique (selon la personnalisation).
- **Gestion des articles configurables** : Utilisation des tables ORDER_CFGS_REF, ORDER_CFGS_INST, ORDER_CFGS_PART_OF, et ORDER_CFGS_VALUE.
- **Transactions avec carte de crédit et PayPal** :
  - Gestion des cartes via la structure BAPICCARD.
  - Transactions PayPal gérées comme les paiements par carte de crédit (type de carte DP2P, fournisseur de services DPPP).
- **Numéro de document** : Renvoi du numéro de document de vente (SALESDOCUMENT) en cas de succès.
- **Erreur** : Les erreurs sont renvoyées via le paramètre RETURN.
- **Zone de vente** : Si elle n'est pas définie, elle est déterminée automatiquement à partir des données du partenaire (client principal ou de livraison).
- **Commit de base de données** : Nécessite un appel explicite à la BAPI BAPI_TRANSACTION_COMMIT pour valider les modifications dans la base de données.
