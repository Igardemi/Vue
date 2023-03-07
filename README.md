# Directivas
Una directiva es un atributo especial que comienza con el v-prefijo. Son parte de la sintaxis de la plantilla de Vue. Al igual que las interpolaciones de texto, los valores de las directivas son expresiones de JavaScript que tienen acceso al estado del componente. 

# v-bind
Para vincular un atributo a un valor dinámico, usamos la v-bind para vincular con una variable del script.
<div v-bind:id="dynamicId"></div>
tiene una sintaxis abreviada dedicada:
<div :id="dynamicId"></div>

# v-on
Podemos escuchar eventos DOM usando la v-on directiva:
<button v-on:click="increment">{{ count }}</button>
tiene una sintaxis abreviada:
<button @click="increment">{{ count }}</button>


# v-model
sincroniza automáticamente el <input> valor de con el estado enlazado, por lo que ya no necesitamos usar un controlador de eventos para eso.

sustituye:
<input :value="text" @input="onInput">
methods: {
  onInput(e) {
    // a v-on handler receives the native DOM event
    // as the argument.
    this.text = e.target.value
  }
}
por:
<input v-model="text">


# v-if
Podemos usar la v-if directiva para representar condicionalmente un elemento.
<h1 v-if="awesome">Vue is awesome!</h1>
Esto <h1>se representará solo si el valor de awesomees verdadero . Si awesomecambia a un valor falso , se eliminará del DOM.
También podemos usar v-elsey v-else-ifpara denotar otras ramas de la condición:
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>

# v-for

Podemos usar la v-fordirectiva para generar una lista de elementos basada en una matriz fuente:
<ul>
  <li v-for="todo in todos" :key="todo.id">
    {{ todo.text }}
  </li>
</ul>
 también estamos dando a cada objeto todo un único idy vinculándolo como el atributo especial key para cada uno <li>.  El keypermite a Vue mover con precisión cada uno <li>para que coincida con la posición de su objeto correspondiente en la matriz.



 # Ciclo de Vida
Habrá casos en los que necesitemos trabajar manualmente con el DOM.
Podemos solicitar una referencia de plantilla , es decir, una referencia a un elemento de la plantilla, utilizando el atributo especial ref.
El elemento se expondrá como this.$refs.p . Sin embargo, solo puede acceder a él después de montar el componente .

Para ejecutar el código después del montaje, podemos usar la mounted opción, Hay otros ganchos como created y updated:

 <script>
export default {
  mounted() {
   this.$refs.p.textContent= 'mounted!'
  } 
}
</script>

<template>
  <p ref="p">hello</p>
</template>

# Vigilantes
A veces, es posible que necesitemos realizar "efectos secundarios" de forma reactiva, por ejemplo, registrar un número en la consola cuando cambia. Podemos lograr esto con los observadores:

export default {
  data() {
    return {
      count: 0
    }
  },
  watch: {
    count(newCount) {
      // yes, console.log() is a side effect
      console.log(`new count is: ${newCount}`)
    }
  }

Aquí, estamos usando la watchopción para ver los cambios en la countpropiedad. La devolución de llamada del reloj se llama cuando countcambia y recibe el nuevo valor como argumento.


# Componentes
Para usar un componente secundario, primero debemos importarlo y luego, podemos usar el componente en la plantilla como: <ChildComp />

<script>
  import ChildComp from './ChildComp.vue'
  
export default {
  components: {
    ChildComp
  }
}
</script>

<template>
  <ChildComp />
</template>

# Accesorios COMUNICACION PADRE HIJO

Un componente hijo puede aceptar entradas del padre a través de accesorios . Primero, necesita declarar los accesorios que acepta:

// in child component
export default {
  props: {
    msg: String
  }
}

padre puede pasar la propiedad al hijo como si fueran atributos. Para pasar un valor dinámico, también podemos usar la v-bind sintaxis:

<ChildComp :msg="greeting" />

Ejemplo:

**Padre**

<script>
import ChildComp from './ChildComp.vue'

export default {
  components: {
    ChildComp
  },
  data() {
    return {
      greeting: 'Hi'
    }
  }
}
</script>

<template>
  <ChildComp :msg="greeting" />
</template>

**Hijo:**
<script>
export default {
  props: {
    msg: String
  }
}
</script>

<template>
  <h2>{{ msg || 'No props passed yet' }}</h2>
</template>


# Accesorios COMUNICACION HIJO PADRE

Además de recibir accesorios, un componente secundario también puede emitir eventos al principal:

export default {
  // declare emitted events
   emits: ['response'],
  created() {
    // emit with argument
    this.$emit('response', 'hello from child')
  }
}

El primer argumento para es el nombre del evento. Cualquier argumento adicional se pasa al detector de eventos.this.$emit()

El padre puede escuchar los eventos emitidos por el niño usando v-on: aquí el controlador recibe el argumento adicional de la llamada de emisión del niño y lo asigna al estado local:
<ChildComp @response="(msg) => childMsg = msg" />



Comandos:

 iniciar proyecto: npm init vue@latest
 npm install
 npm run dev
