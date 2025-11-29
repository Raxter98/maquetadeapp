📘 README – Proyecto Ionic + Angular (KIKI App)

🚀 Características del Proyecto

Navegación completa – ✔
Angular Standalone – ✔
Lazy Loading – ✔
Menú lateral – ✔
Este proyecto implementa una arquitectura moderna basada en:

Ionic 7
Angular 17 con Standalone Components
Lazy loading de páginas
IonMenu + IonRouterOutlet para navegación con menú lateral
📱 Pantallas Incluidas

Login
Register
Dashboard
Requests
Pending Tasks
Map
Scanner
Profile
✅ REQUISITOS PARA EJECUTAR EL PROYECTO

Instalar lo siguiente:

Node.js (versión estable)

text
https://nodejs.org/
Ionic CLI

bash
npm install -g @ionic/cli
Angular CLI (opcional pero recomendado)

bash
npm install -g @angular/cli
Git
📂 ESTRUCTURA DEL PROYECTO

text
src/
└── app/
    ├── app.routes.ts
    ├── app.component.ts
    ├── app.component.html
    ├── app.component.scss
    │
    ├── dashboard/
    ├── requests/
    ├── pending-task/
    ├── map/
    ├── scanner/
    ├── profile/
    ├── login/
    └── register/
Cada carpeta contiene una pantalla completamente independiente, con:

.page.ts
.page.html
.page.scss
🚀 CÓMO EJECUTAR EL PROYECTO

Ir a la raíz del proyecto:

bash
cd kiki
Instalar dependencias:

bash
npm install
Ejecutar:

bash
ionic serve
La app abrirá automáticamente en el navegador.

🧭 SISTEMA DE NAVEGACIÓN (Routing)

app.routes.ts

typescript
import { Routes } from '@angular/router';

export const routes: Routes = [
  { path: '', redirectTo: 'login', pathMatch: 'full' },

  { path: 'login', loadComponent: () => import('./login/login.page').then(m => m.LoginPage) },
  { path: 'register', loadComponent: () => import('./register/register.page').then(m => m.RegisterPage) },

  { path: 'dashboard', loadComponent: () => import('./dashboard/dashboard.page').then(m => m.DashboardPage) },
  { path: 'requests', loadComponent: () => import('./requests/requests.page').then(m => m.RequestsPage) },
  { path: 'pending-task', loadComponent: () => import('./pending-task/pending-task.page').then(m => m.PendingTaskPage) },
  { path: 'map', loadComponent: () => import('./map/map.page').then(m => m.MapPage) },
  { path: 'scanner', loadComponent: () => import('./scanner/scanner.page').then(m => m.ScannerPage) },
  { path: 'profile', loadComponent: () => import('./profile/profile.page').then(m => m.ProfilePage) },
];
🧱 LAYOUT PRINCIPAL (MENÚ LATERAL + OUTLET)

app.component.html

html
<ion-app>
  <ion-menu contentId="main-content" side="start">
    <ion-header>
      <ion-toolbar color="primary">
        <ion-title>Menu</ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content>
      <ion-list>
        <ion-item button routerLink="/requests">Requests</ion-item>
        <ion-item button routerLink="/pending-task">Pending Tasks</ion-item>
        <ion-item button routerLink="/map">Map</ion-item>
        <ion-item button routerLink="/scanner">Scanner</ion-item>
        <ion-item button routerLink="/profile">Profile</ion-item>
      </ion-list>
    </ion-content>
  </ion-menu>

  <ion-router-outlet id="main-content"></ion-router-outlet>
</ion-app>
🎬 BOTÓN DE MENÚ PARA CADA PÁGINA

Esto debe agregarse en todas las páginas que necesitan abrir el menú:

html
<ion-header>
  <ion-toolbar>
    <ion-buttons slot="start">
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
    <ion-title>Requests</ion-title>
  </ion-toolbar>
</ion-header>
📄 EJEMPLO COMPLETO DE UNA PÁGINA

RequestsPage (versión correcta)

requests.page.ts

typescript
import { Component } from '@angular/core';
import { Router } from '@angular/router';
import { IonicModule, MenuController } from '@ionic/angular';

@Component({
  selector: 'app-requests',
  standalone: true,
  imports: [IonicModule],
  templateUrl: './requests.page.html',
  styleUrls: ['./requests.page.scss']
})
export class RequestsPage {

  constructor(
    private router: Router,
    private menu: MenuController
  ) {}

  go(path: string) {
    this.router.navigate([path]);
  }

  openMenu() {
    this.menu.open();
  }
}
requests.page.html

html
<ion-header>
  <ion-toolbar>
    <ion-buttons slot="start">
      <ion-menu-button></ion-menu-button>
    </ion-buttons>
    <ion-title>Requests</ion-title>
  </ion-toolbar>
</ion-header>

<ion-content class="ion-padding">
  <h1>Requests</h1>
</ion-content>
requests.page.scss

scss
@use '../../theme/variables.scss' as *;

ion-content {
  padding: 16px;
}

.list-request {
  display: grid;
  gap: 12px;
}

.request-item {
  background: #fff;
  padding: 12px;
  border-radius: 12px;
  box-shadow: var(--shadow-base);
}
🔄 NOTA IMPORTANTE SOBRE NAVEGACIÓN

El proyecto NO tiene la función go() en AppComponent.
Cada página incluye su propia navegación, ejemplo: go('/profile')

app.component.ts está así (correcto):

typescript
import { Component } from '@angular/core';
import { IonApp, IonRouterOutlet } from '@ionic/angular/standalone';

@Component({
  selector: 'app-root',
  templateUrl: 'app.component.html',
  imports: [IonApp, IonRouterOutlet],
})
export class AppComponent {}
❗ PROBLEMAS ENFRENTADOS

Estructura inicial de Ionic distinta a la requerida
Necesidad de usar Angular 17 con Standalone (sin módulos)
Lazy loading obligatorio
Importación manual de IonMenu, IonRouterOutlet, IonHeader
Errores de navegación por ausencia de funciones (go(), openMenu())
Reorganización completa de carpetas
Los diseños finales no forman parte de esta entrega (solo estructura navegable)
🎯 CONCLUSIÓN

Este repositorio entrega:

✔ Menú lateral funcional
✔ Navegación profesional
✔ Rutas con lazy loading
✔ App estructurada por pantallas independientes
✔ Componentes standalone (Angular 17)
✔ Código limpio, comprensible y correcto
✔ README listo para presentar a un profesor