# React Shopping Cart

Shopping cart app built with React and Firebase. Currently WIP.

This app is a clone of https://alphaleteathletics.com.

## App Preview

https://github.com/jp-quintana/react-shopping-cart/assets/87621233/049ad637-aea3-4a8a-8c32-51abbc59fb9d

_(Version in video deployed Jul 27, 2023)_

## Features

- Products Display.
- Products Filter.
- Infinite Scroll.
- Cart Functions.
- Basic Inventory Management.
- Auth (Email/Password & Anonymous).
- Mock Checkout Page.
- User orders & addresses.

## Future additions

Check issues tab.

## Installation

- Step 1: Clone Repository and Install Packages.

```
git clone https://github.com/jp-quintana/flaakko-shopping-cart.git && npm install
```

- Step 2: Create firebase-config.js file inside src/firebase directory.

```
export const firebaseConfig = {
  apiKey: '',
  authDomain: '',
  databaseURL: '',
  projectId: '',
  storageBucket: '',
  messagingSenderId: '',
  appId: '',
};
```

- Step 3: Start the development server.

```
npm run dev
```

## Setup Firebase Project

### Firestore
Create products and users collections and carts, checkoutSessions and orders ones optionally.

#### Products Collection
![products-collection](https://github.com/jp-quintana/react-shopping-cart/assets/87621233/63f443f1-a6e4-4c02-8c57-4b247fc5b7be)
Product collection holds both variants and skus collection.
- collection: must match one of the allowed skus in CollectionPage component.
- price: sets actual price. Variant doc handles discount logic.

#### Variants Subcollection
![variants-subcollection-1](https://github.com/jp-quintana/react-shopping-cart/assets/87621233/128cd824-87b9-4cda-9af6-24e6989ea100)
Each variant represents a different color.
- productId: should hold parent doc id.
- images: same id as folder which contains corresponding variant image in cloude storage. And src should be the link provided by cloud storage when uploading corresponding image.
- variantPrice: should hold a number equal or less to product price. If variantPrice < price, then the product variant will be showed as "on sale" in UI.

#### Skus Subcollection
![skus-subcollection-1](https://github.com/jp-quintana/react-shopping-cart/assets/87621233/439d36fc-bb9b-4a3c-b03c-a4d47a58176c)
Although these docs are children of product doc, skus are specific to the product variant, not the product itself. Say for example, if variant has 5 sizes, there should be 5 sku docs, each one representing a different size. If the product has 2 colors, each with 5 sizes, you need to create 10 sku docs.
- productId: should hold parent doc id.
- variantId: should hold corresponding variant doc id.
- value: this is the sku value. It's currently not used in the app itself. App uses the sku doc id generated by firebase.

### Cloud Storage
![cloud-storage-example](https://github.com/jp-quintana/react-shopping-cart/assets/87621233/3b2d8c98-a20e-4332-9ce8-494a3e2c90e8)
Each image should be stored in a folder with a name that corresponds to its respective ID. Aditionally each image folder should be stored in the "product-images" repository. The "src" is obtained by clicking the link inside the red rectangle. See image above and the one in Variants Subcollection section.


## Admin View
![admin-view](https://github.com/jp-quintana/react-shopping-cart/assets/87621233/187acbd1-8704-4d40-892c-06c3cdabac34)

_(Can be found in App.jsx in src folder)_

### Note 
Important: comment out all admin routes before deploying app as firestore rules are not configured yet. Commented out lines in image above currently do not work even though components are found in project.

### Seed Data to Firebase

#### Setup Admin
![is-admin](https://github.com/jp-quintana/react-shopping-cart/assets/87621233/8ab844a3-e102-4846-bcf1-0b3d2846db6e)
Create new user in the app and add "isAdmin: true" to corresponding user doc in firestore. 

#### Data
![seed-data](https://github.com/jp-quintana/react-shopping-cart/assets/87621233/9b3bc7f6-76e2-4fa5-9c5b-b799a8920531)
Use "dummy-products.json" file in data folder as guide for your own data. At the moment you must add each image manually to the cloud storage as shown above and afterwards add the corresponding links to the json file. Once you've added your data, change file name to "products.json".


## Authors

- [@jp-quintana](https://github.com/jp-quintana)
