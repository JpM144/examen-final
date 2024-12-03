
document.addEventListener("DOMContentLoaded", () => {
  const estadoCivil = document.getElementById("estadoCivil");
  const compañeroInfo = document.getElementById("compañeroInfo");
  const tieneHijos = document.getElementById("tieneHijos");
  const hijosInfo = document.getElementById("hijosInfo");
  const cantidadHijos = document.getElementById("cantidadHijos");
  const hijosContainer = document.getElementById("hijosContainer");
  const subsidioMensaje = document.getElementById("subsidioMensaje");
  const sexo = document.getElementById("sexo");

  const departamentoSelect = document.getElementById("departamento");
  const ciudadSelect = document.getElementById("ciudad");

  let departamentosCiudades;

  // Cargar departamentos y ciudades desde JSON
  fetch("departm.json")
    .then((response) => response.json())
    .then((data) => {
      departamentosCiudades = data;
      data.forEach((dep) => {
        const option = document.createElement("option");
        option.value = dep.nombre;
        option.textContent = dep.nombre;
        departamentoSelect.appendChild(option);
      });
    });

  departamentoSelect.addEventListener("change", () => {
    const selectedDep = departamentoSelect.value;
    const ciudades = departamentosCiudades.find(
      (dep) => dep.nombre === selectedDep
    ).ciudades;

    ciudadSelect.innerHTML = "<option value='' selected disabled>Seleccione una ciudad</option>";
    ciudades.forEach((ciudad) => {
      const option = document.createElement("option");
      option.value = ciudad;
      option.textContent = ciudad;
      ciudadSelect.appendChild(option);
    });
  });

  // Mostrar campos de compañero/conyugue
  estadoCivil.addEventListener("change", () => {
    compañeroInfo.classList.toggle("d-none", estadoCivil.value === "soltero");
  });

  // Mostrar campos para hijos
  tieneHijos.addEventListener("change", () => {
    hijosInfo.classList.toggle("d-none", tieneHijos.value !== "si");
    if (tieneHijos.value === "no") {
      hijosContainer.innerHTML = "";
      subsidioMensaje.textContent = "";
    }
  });

  cantidadHijos.addEventListener("input", () => {
    const numHijos = parseInt(cantidadHijos.value, 10);
    hijosContainer.innerHTML = "";
    subsidioMensaje.textContent = "";

    if (!isNaN(numHijos) && numHijos > 0) {
      for (let i = 0; i < numHijos; i++) {
        const div = document.createElement("div");
        div.className = "mb-3";
        div.innerHTML = `
          <label for="hijo${i}" class="form-label">Nombre del Hijo ${i + 1}</label>
          <input type="text" id="hijo${i}" class="form-control" required>
        `;
        hijosContainer.appendChild(div);
      }

      if (sexo.value === "F") {
        subsidioMensaje.textContent = `¡Puede acceder a un subsidio por sus ${numHijos} hijos!`;
      }
    }
  });
});
