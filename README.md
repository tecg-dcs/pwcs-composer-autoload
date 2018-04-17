# Autoloading PSR-4 avec Composer

Ce fichier est un petit squelette minimal pour montrer l’autoloading par composer selon la norme psr-4

- Imaginons que dans le fichier `index.php`, situé à la racine du projet, nous voulions écrire le nom de la classe dont est issue une instance :
```php
echo get_class(new MaClasse());
```
- cette classe (`MaClasse`) est définie dans un fichier du même nom stocké dans le répertoire `classes` situé à la racine du projet. Nous allons décider de faire correspondre à ce répertoire un espace de noms, celui de notre application par exemple. Appelons-le `Acme`. Au début de la classe, nous renseignons donc l’espace de noms : 
```php
namespace Acme;
```
- dans notre fichier index.php, nous devons importer la classe. Mais nous ne le faisons pas en incluant le fichier qui la contient. Au lieu de ça, nous l’importons en fonction de l’espace de noms dans lequel elle est définie : `use Acme\MaClasse;`. C’est composer qui fera la traduction entre l’espace de noms `Acme` et le dossier `classes` ;
- dans le fichier `composer.json`, nous définissons le mapping entre l’espace de noms et le dossier. Nous ajoutons une clé dans l’objet qui décrit notre projet composer : 
```json 
"autoload": { "psr-4": { "Acme\\": "classes/" }}
```
- une fois le fichier composer.json mis à jour, on demande à composer de mettre à jour le fichier php qui contient les directives qui font véritablement l’autoload : 
```php
composer dumpautoload
```
- enfin, il ne faut pas oublier d’ajouter dans le fichier `index.php` l’instruction qui inclut le fichier d’autoload produit par composer : 
```php
require "vendor/autoload.php";
```
