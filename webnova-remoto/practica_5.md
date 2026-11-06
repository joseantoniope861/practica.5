# Práctica 5. Colaboración en GitHub y Resolución de Conflictos Remotos - Entregable

**Alumno/a:** [Tu Nombre y Apellidos]  
**Fecha:** 2026-11-06  

---

## 1. Captura 1: Error `! [rejected]` al hacer `git push`

En la Fase 3, al intentar subir nuestros cambios locales sin habernos sincronizado previamente con el repositorio remoto, Git rechaza la operación para evitar sobrescribir el trabajo del compañero.

![Captura 1: Error de rechazo en el push](1)

---

## 2. Captura 2: Marcas de Conflicto en el Editor de Código

Durante el proceso de `git pull --rebase`, Git detecta que la misma línea ha sido modificada tanto en el servidor como localmente, deteniendo el proceso y mostrando las marcas de conflicto (`<<<<<<<`, `=======`, `>>>>>>>`).

![Captura 2: Marcas de conflicto en el archivo equipo.md](2)

---

## 3. Captura 3: Repositorio en GitHub con el Resultado Final

Una vez aplicado `git add`, `git rebase --continue` y el `git push` definitivo, el archivo en la interfaz web de GitHub muestra la integración completa y correcta de ambos miembros.

![Captura 3: Repositorio en GitHub finalizado](3)

---

## 4. Pregunta de Reflexión

### ¿Por qué Git bloqueó tu subida en la Fase 3?
Git bloqueó la subida (`push`) porque el repositorio remoto (`origin/main`) se encontraba en un estado más avanzado o divergente respecto al commit local desde el cual partíamos. Al haber realizado un commit en la nube (el del compañero) y otro commit en local de forma independiente sobre la misma línea temporal, Git detecta que subir nuestros cambios directamente sobrescribiría o eliminaría el trabajo del servidor sin tenerlo en cuenta. El principio fundamental de Git es no perder información de manera silenciosa, por lo que exige sincronizarse primero.

### ¿Qué ventaja tiene usar `git pull --rebase` en lugar de un simple `git pull` en estos casos?
La principal ventaja de utilizar `git pull --rebase` frente a un `git pull` tradicional (que por defecto hace un `merge`) es **mantener un historial de commits limpio y estrictamente lineal**. 
* Un `git pull` normal crearía un commit de fusión (*merge commit*) adicional y una bifurcación innecesaria en el grafo de commits para unir las dos historias.
* En cambio, `git rebase` toma nuestros commits locales pendientes, "pausa" temporalmente nuestro trabajo, descarga los nuevos commits del repositorio remoto y luego vuelve a aplicar nuestros commits locales **por encima** de los del compañero. Esto evita ramificaciones confusas en proyectos pequeños o medianos y deja una línea de tiempo mucho más clara y profesional.