# Tipti Challenge

## Instalacion
```
Clona el repositorio en tu máquina local
```

### Navega hasta la carpeta del proyecto: cd nombre-del-proyecto.
```
cd challenge
```

### Instala las dependencias
```
npm install
```

### Inicia el servidor de desarrollo
```
npm run serve
```

### Abre tu navegador y visita la siguiente URL para ver el proyecto funcionando
```
http://localhost:8080
```



# Tecnologías utilizadas
```
- HTML
- CSS
- Vue.js
```

# Sobre el desafio

```
Pensé el desafio como una forma de mostrar variedad de técnicas de vue para completarlo. Si bien no es un desafío muy complejo,
intenté utilizar varias caracteristicas de Vue,js tanto como methods, computed properties, props, events, directivas como v-for,
v-if, v-show, v-bind, v-model, algo de ciclo de vida con mounted, etc. Pensé usar Vuex o Router pero hubiese complejizado de más
la solución.
La estructura del proyecto se compone del App.vue como componente padre y referente, en él se aplica la lógica principal del desafío,
filtrar la mejor opción de hotel, pero la información del hotel, las fechas y el tipo de usuario son otorgados a través de eventos de
sus 3 componentes hijos : InputDate.vue, SelectUserType.vue y HotelOption.Vue, este último con un componente hijo adicional, CardView.Vue,
ya que se deben mostrar tarjetas con cierta informacion de hoteles cuando están todos a la vista pero cuando se filtra y se muestra uno solo
se debe mostrar otro tipo de información, entonces los estilos hechos en CardView.vue aplican perfectamente para ambos casos.
Cada componente tiene su propia lógica para lograr los resultados esperados, se aplicaron validaciones para que no se pueda avanzar en caso
de que alguna de las fechas estén vacias o repetidas. 
Una vez que se pasa las validaciones y se filtra el mejor hotel, decidí permitir la posibilidad de seguir cambiando el tipo de usuario
y las fechas para que reactivamente un watch vaya actualizando la card de mejor opción, en caso de vaciar una fecha o repetirla, la card
desaparecerá y mostrará un mensaje de error hasta que se resuelva el conflicto.

```