# **Function Scope JS**

[![forthebadge](http://forthebadge.com/images/badges/built-by-developers.svg)](http://forthebadge.com)
[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com)
[![forthebadge](http://forthebadge.com/images/badges/for-you.svg)](http://forthebadge.com)

## **Descripción**

En el presente trabajo, se ha realizado un análisis del código en el archivo `app.js` identificando los tipos de variable según scope, tipos de funciones, closure, etc. para demostrar lo aprendio en este sprint.

## **Análisis**

### **Código a analizar**

```bash
$(document).ready(function() {

  console.log('Probar con el numero valido 4544164785372342');
  
  // Declaramos las variables que vamos a utilizar
  var $inputCard = $('#card-number');
  var $inputMonth = $('.input-month');
  var $inputYear = $('.input-year');
  var $buttonNext = $('#next');
  var regexOnlyNumbers = /^[0-9]+$/;
  var labelErrorOrSuccessMessages = $('label[for="card-number"]');

  // Identificar el evento que nos permite capturar el input del usuario
  $inputCard.on('input', function() {
    isValidCreditCard($(this).val().trim());
  });

  // Funciones que habilita el boton del formulario
  function activeButton() {
    $buttonNext.attr('disabled', false);
  }

  // Funcion que desabilita el boton del formulario
  function desactiveButton() {
    $buttonNext.attr('disabled', true);
  }

  // Funcion que valida la longitud del input ingresado por el usuario
  function longitud(input) {
    if (input.trim().length === 16) {
      return input;
    }
  }

  // Funcion que valida la longitud del input ingresado por el usuario
  function soloNumeros(input) {
    var regex = /^[0-9]+$/;
    if (regex.test(input)) {
      return input;
    }
  }

  // Funcion que valida que sea una un numero de tarjeta valido   
  function isValidCreditCard(numberCard) {
    var creditCardNumber = soloNumeros(longitud(numberCard));
    if (creditCardNumber !== undefined) {
      var arr = [];
      var sumaTotal = 0;
      for (var index = creditCardNumber.length - 1; index >= 0; index--) {
        arr.push(creditCardNumber[index]);
      }
      for (var index = 1; index < arr.length; index = index + 2) {
        arr[index] = arr[index] * 2;
        if (arr[index] >= 10) {
          arr[index] = arr[index] - 9;
        }
      }

      for (var index = 0; index < arr.length; index++) {
        sumaTotal = sumaTotal + parseInt(arr[index]);
      }

      if (sumaTotal % 10 === 0) {
        console.log('Es una tarjeta valida');
        activeButton();
      } else {
        console.log('No es un numero valido');
        desactiveButton();
      }
    } else {
      console.log('Verifique el numero de su tarjeta'); 
      desactiveButton();
    }
  }
});

```

### **Variables**

Las variables que se presentan a continuación son `variables locales` porque están dentro de la función del evento ready(`$(document).ready(function() {...}`). No obstante para las funciones que están contenidas dentro del scope de esta `función global`, estas variables son `variables globales`.

```bash
var $inputCard = $('#card-number');
var $inputMonth = $('.input-month');
var $inputYear = $('.input-year');
var $buttonNext = $('#next');
var regexOnlyNumbers = /^[0-9]+$/;
var labelErrorOrSuccessMessages = $('label[for="card-number"]');
```

Tomando en cuenta este último punto de vista:

La variable regex es una `variable local`, ya que está contenida dentro una función llamada **soloNumeros**:

```bash
  function soloNumeros(input) {
    var regex = /^[0-9]+$/;
    if (regex.test(input)) {
      return input;
    }
  }
```

Asimismo, las variables `arr` y `sumaTotal` son `variables locales` por la misma razón:

```bash
function isValidCreditCard(numberCard) {
    var creditCardNumber = soloNumeros(longitud(numberCard));
    if (creditCardNumber !== undefined) {
      var arr = [];
      var sumaTotal = 0;
      for (var index = creditCardNumber.length - 1; index >= 0; index--) {
        arr.push(creditCardNumber[index]);
      }
      ...
```

### **Funciones**

### **Según la manera en que fueron definidas**

#### **Function Statement**

Las funciones `activeButton`, `desactiveButton`, `longitud`, `soloNumeros` y `isValidCreditCard` son funciones statements porque son totalmente disponibles desde cualquier parte del código. No están almacenadas en variables(`function expressions`).

```bash
// Funciones que habilita el boton del formulario
  function activeButton() {
    $buttonNext.attr('disabled', false);
  }

// Funcion que desabilita el boton del formulario
  function desactiveButton() {
    $buttonNext.attr('disabled', true);
  }

  // Funcion que valida la longitud del input ingresado por el usuario
  function longitud(input) {
    if (input.trim().length === 16) {
      return input;
    }
  }

  // Funcion que valida la longitud del input ingresado por el usuario
  function soloNumeros(input) {
    var regex = /^[0-9]+$/;
    if (regex.test(input)) {
      return input;
    }
  }

  // Funcion que valida que sea una un numero de tarjeta valido
  function isValidCreditCard(numberCard) {
    var creditCardNumber = soloNumeros(longitud(numberCard));
    if (creditCardNumber !== undefined) {
      var arr = [];
      var sumaTotal = 0;
      for (var index = creditCardNumber.length - 1; index >= 0; index--) {
        arr.push(creditCardNumber[index]);
      }
      for (var index = 1; index < arr.length; index = index + 2) {
        arr[index] = arr[index] * 2;
        if (arr[index] >= 10) {
          arr[index] = arr[index] - 9;
        }
      }
      ...
```

### **Function Expressions**

Funciones que son almacenadas en variables y pueden ser invocadas por estas. El presente código no contiene funciones de este tipo.

### **Según si tienen nombre**

#### **Funciones nombradas**

Poseen nombre: `activeButton`, `desactiveButton`, `longitud`, `soloNumeros` y `isValidCreditCard`.

```bash
// Funciones que habilita el boton del formulario
  function activeButton() {
    $buttonNext.attr('disabled', false);
  }

  // Funcion que desabilita el boton del formulario
  function desactiveButton() {
    $buttonNext.attr('disabled', true);
  }

  // Funcion que valida la longitud del input ingresado por el usuario
  function longitud(input) {
    if (input.trim().length === 16) {
      return input;
    }
  }

  // Funcion que valida la longitud del input ingresado por el usuario
  function soloNumeros(input) {
    var regex = /^[0-9]+$/;
    if (regex.test(input)) {
      return input;
    }
  }

  // Funcion que valida que sea una un numero de tarjeta valido
  function isValidCreditCard(numberCard) {
    var creditCardNumber = soloNumeros(longitud(numberCard));
    if (creditCardNumber !== undefined) {
      var arr = [];
      var sumaTotal = 0;
      for (var index = creditCardNumber.length - 1; index >= 0; index--) {
        arr.push(creditCardNumber[index]);
      }
      for (var index = 1; index < arr.length; index = index + 2) {
        arr[index] = arr[index] * 2;
        if (arr[index] >= 10) {
          arr[index] = arr[index] - 9;
        }
      }
      ...
```

#### **Funciones anónimas**

Son funciones que no poseen nombre. Para definirlas solo se escribe la palabra reservada **function**, seguida de paréntesis.

```bash
$(document).ready(function() {
  ...
}
```

```bash
$inputCard.on('input', function() {
    isValidCreditCard($(this).val().trim());
  });
```

### **Según el scope**

