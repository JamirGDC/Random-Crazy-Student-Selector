# Random-Crazy-Student-Selector


### Before
```
const listaPersonas = [
{ nombre: "Maria" },
{ nombre: "Paul" },
{ nombre: "Jamir" },
{ nombre: "Agustin" }
];

function imprimirPersona() {
    const contenedor = document.getElementById("personas");
    const personasOrder = listaPersonas.sort((a, b) => a.nombre.localeCompare(b.nombre));

    personasOrder.forEach(persona => {
        const checkbox = document.createElement("input");
        checkbox.type = "checkbox";
        checkbox.name = persona.nombre;
        contenedor.appendChild(checkbox);

        const label = document.createElement("label");
        label.innerHTML = persona.nombre;
        contenedor.appendChild(label);

        contenedor.appendChild(document.createElement("br"));

    });
}
imprimirPersona();




```




### After

```
const listaPersonas = [
    { nombre: "Maria" },
    { nombre: "Paul" },
    { nombre: "Jamir" },
    { nombre: "Agustin" }
];
const contenedorPersonasEnHtml = document.getElementById("listaDePersonas");

function mostrarListaDePersonas() {

    const listaOrdenada = ordenarListaInicial(obtenerListaDePersonas());
    mostrarListaEnHTML(listaOrdenada);
};

function obtenerListaDePersonas() {
    return listaPersonas;
};

function ordenarListaInicial(listaInicial) {
    return listaInicial.slice().sort((persona1, persona2) => persona1.nombre.localeCompare(persona2.nombre));
}

function crearCheckBox(persona) {
    const checkbox = document.createElement("input");
    checkbox.type = "checkbox";
    checkbox.id = persona.nombre;
    checkbox.name = persona.nombre;
    checkbox.value = persona.nombre;
    return checkbox;
}

function crearLabel(persona) {
    const label = document.createElement("label");
    label.htmlFor = persona.nombre;
    label.appendChild(document.createTextNode(persona.nombre));
    return label;
}

function mostrarListaEnHTML(listaOrdenada) {
    listaOrdenada.forEach(persona => {
        const checkbox = crearCheckBox(persona);
        const label = crearLabel(persona);
        contenedorPersonasEnHtml.appendChild(checkbox);
        contenedorPersonasEnHtml.appendChild(label);
        contenedorPersonasEnHtml.appendChild(document.createElement("br"));
    });

}

function obtenerPersonasSeleccionadas() {
    const checkBoxSeleccionados = contenedorPersonasEnHtml.querySelectorAll('input[type="checkbox"]:checked');
    const personasSeleccionadas = [];
    checkBoxSeleccionados.forEach(checkBox => {
        const persona = listaPersonas.find(persona => persona.nombre === checkBox.value);
        personasSeleccionadas.push(persona);
    });
    return personasSeleccionadas;
};

function elegirPersona() {
    const personasSeleccionadas = obtenerPersonasSeleccionadas();
    const personaElegida = personasSeleccionadas[Math.floor(Math.random() * personasSeleccionadas.length)];
    if (personaElegida) {
        alert(`La persona elegida es ${personaElegida.nombre}`);
    }
    else {
        alert("No se ha seleccionado ninguna persona");
    }
}

mostrarListaDePersonas();




```
