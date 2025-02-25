# Système d'authentification Laravel from scratch avec validation de register via Middleware

Ce projet consiste à implémenter un système d'authentification en Laravel sans utiliser les packages d'authentification préfaits, en validant l'inscription (
register) à l'aide d'un middleware.

## Prérequis
- PHP ≥ 8.0
- Composer
- Laravel ≥ 9.x
- Une base de données configurée

## Installation
Suivez les étapes ci-dessous pour mettre en place le projet :

### 1. Créer un Projet Laravel
```bash
composer create-project laravel/laravel NomDuProjet
cd NomDuProjet
```

### 2. Configuration de la Base de Données
Assurez-vous que le fichier `.env` est correctement configuré :
```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=nom_de_votre_base
DB_USERNAME=votre_utilisateur
DB_PASSWORD=votre_mot_de_passe
```

### 3. Exécuter les Migrations
```bash
php artisan migrate
```

### 4. Création des Contrôleurs d'Authentification
Générez les contrôleurs `LoginController` et `RegisterController` :
```bash
php artisan make:controller Auth/LoginController
php artisan make:controller Auth/RegisterController
```
Ajoutez la logique d'authentification et d'inscription dans ces contrôleurs.

### 5. Création du Middleware de Validation (`ValidateRegisterMiddleware`)
```bash
php artisan make:middleware ValidateRegisterMiddleware
```
Dans `app/Http/Middleware/ValidateRegisterMiddleware.php`, ajoutez la logique de validation des données d'inscription.

### 6. Enregistrement du Middleware dans `Kernel.php`
Ajoutez le middleware dans `app/Http/Kernel.php` :
```php
protected $routeMiddleware = [
    'validate.register' => \App\Http\Middleware\ValidateRegisterMiddleware::class,
];
```

### 7. Utilisation du Middleware dans les Routes
Dans `routes/web.php`, appliquez le middleware aux routes concernées :
```php
Route::post('/register', [RegisterController::class, 'store'])->middleware('validate.register');
```

## Exécution
Lancez le serveur Laravel :
```bash
php artisan serve
```
Puis accédez à l'application via `http://127.0.0.1:8000`.

## Auteur
- **[Ton Nom]** - Développeur Laravel

## Licence
Ce projet est sous licence MIT.

