# Ionic 3 Multi Language Example

Step 1: Start new ionic app:
1. ionic start multilingual tabs
2.  cd multilingual
Step 2: Install angular translate library in ionic app:
3. npm install @ngx-translate/core @ngx-translate/http-loader --save 
 or this if Angular 5

3. npm install @ngx-translate/core@^9.1.1 @ngx-translate/http-loader -–save
Now edit app.module.ts file.

Add this line.

import { TranslateModule } from '@ngx-translate/core';
Add this into imports block

imports: [
BrowserModule,
IonicModule.forRoot(MyApp),
TranslateModule.forRoot()
],
 

Step 3: Setting up folder location for languages
Add src/assets/i18n/ folder then add these code in app.modules.ts file.

import { TranslateModule, TranslateLoader } from '@ngx-translate/core';
import { HttpClientModule, HttpClient } from '@angular/common/http';
import { TranslateHttpLoader } from '@ngx-translate/http-loader';

export function setTranslateLoader(http: Http) {
return new TranslateHttpLoader(http, './assets/i18n/', '.json');
}


imports: [
BrowserModule,
IonicModule.forRoot(MyApp),
HttpClientModule,
TranslateModule.forRoot({
loader: {
provide: TranslateLoader,
useFactory: (setTranslateLoader),
deps: [HttpClient]
}
})
],
 

Step 4: Using Translate Service in App
Edit app.component.ts and add these code.

import { TranslateService } from '@ngx-translate/core';

export class MyApp {
rootPage:any = TabsPage;

constructor(platform: Platform, statusBar: StatusBar, splashScreen: SplashScreen, translate: TranslateService) {
translate.setDefaultLang('en');
platform.ready().then(() => {
statusBar.styleDefault();
splashScreen.hide();
});
}
}
Step 5: Add Language Files in i18n folder
Create 3 json files or as required

en.json
de.json
zh_Hans.json
en.json

{
"home":"Home",
"about": "About",
"contact": "Contact",
"welcome":"Welcome to ionic"
}
de.json

{
"home": "huis",
"about": "over",
"contact": "Contact",
"welcome":"Willkommen bei ionischen"
}
zh_Hans.json

{
"home": "家",
"about": "关于",
"contact": "联系",
"welcome":"欢迎来到离子"
}

 

Step 6: Translating Text in App
Now make following changes in given file to use translation.


 
pages/home/home.html

<ion-header>
<ion-navbar>
<ion-title>{{“home” | translate }}</ion-title>
</ion-navbar>
</ion-header>

<ion-content padding>
<h2>{{“welcome” | translate }}</h2>

<button ion-button block (click)=”changeLanguage(‘en’)”>
Translate to English
</button>

<button ion-button block (click)=”changeLanguage(‘de’)”>
Translate to German
</button>

<button ion-button block (click)=”changeLanguage(‘zh_Hans’)”>
Translate to Chinese 
</button>
</ion-content>

Add this code in

pages/home/home.ts

import { Component } from '@angular/core';
import { NavController } from 'ionic-angular';
import { TranslateService } from '@ngx-translate/core';
@Component({
selector:'page-home',
templateUrl:'home.html'
})
export class HomePage {
constructor(publicnavCtrl:NavController,publictranslateService:TranslateService) {
}
changeLanguage(langauge){
this.translateService.use(langauge);
}
}
Add this code in

pages/tabs/tabs.html

<ion-tabs>
<ion-tab [root]="tab1Root" tabTitle='{{"home" | translate }}' tabIcon="home"></ion-tab>
<ion-tab [root]="tab2Root" tabTitle='{{"about" | translate }}' tabIcon="information-circle"></ion-tab>
<ion-tab [root]="tab3Root" tabTitle='{{"contact" | translate }}' tabIcon="contacts"></ion-tab>
</ion-tabs>
You are all set test your application by running “ionic serve”

If you get some issues you can comment below.
Some issue i found
https://github.com/ngx-translate/http-loader/issues/47
https://github.com/ngx-translate/http-loader/issues/13
Final Result..
Ionic 3 Multi Language Example
Have a great day Happy Coding… 🙂
