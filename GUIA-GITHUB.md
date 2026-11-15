# Guía de trabajo con GitHub

Esta guía explica cómo trabajamos el código de Ovium. Nadie edita `main` ni `develop` directamente: cada tarjeta se trabaja en su propia rama y se une con un **pull request (PR)**, que es una solicitud para que un compañero revise el trabajo antes de unirlo.

## Cuándo una tarjeta está terminada (Definition of Done)

Una tarjeta está **TERMINADA** cuando:

1. El código está en `develop` por pull request.
2. Otro compañero lo revisó y lo aprobó.
3. Las pruebas pasan.
4. Se probó que funciona.

## Cómo se trabaja

- Cada tarjeta = una rama `feature/nombre-de-la-tarjeta`, creada desde `develop`.
- Se abre un pull request hacia `develop` y lo revisa un compañero.
- Nadie sube directo a `main` ni a `develop`.
- Solo Rolando o Walter aprueban lo que pasa a `main`.

## Antes de empezar (una sola vez)

1. Instala **Git** y ten tu cuenta de GitHub dentro de la organización **OVIUM-team**.
2. Clona el repo de tu parte:
   ```
   git clone https://github.com/OVIUM-team/ovium-backend.git
   ```
   Cambia el nombre por `ovium-android`, `ovium-web` o `ovium-docs` según toque.

## Paso a paso por cada tarjeta

**1. Trae lo último de `develop`**
```
git checkout develop
git pull
```

**2. Crea tu rama** con el nombre de la tarjeta
```
git checkout -b feature/api-autenticacion
```

**3. Trabaja y guarda tus cambios** con commits pequeños
```
git add .
git commit -m "Agrega login con JWT"
```

**4. Sube tu rama a GitHub**
```
git push -u origin feature/api-autenticacion
```

**5. Abre el pull request**
- Entra al repo en GitHub. Aparece el botón verde **Compare & pull request**.
- Comprueba que diga: de `feature/...` **hacia `develop`**.
- Escribe qué hiciste y pega el nombre de la tarjeta de Trello.
- En **Reviewers**, elige a un compañero.

**6. Espera la revisión**
Tu compañero revisa y aprueba, o deja comentarios. Si pide cambios, los haces en la misma rama y haces `git push`: el PR se actualiza solo.

**7. Une el PR**
Con la aprobación, pulsa **Merge pull request** y luego **Delete branch**.

**8. Marca la tarjeta** como lista en Trello y pasa a la siguiente.

## Si te toca revisar el PR de otro

1. Abre el PR y entra a **Files changed**.
2. Lee los cambios. Puedes comentar una línea concreta.
3. Arriba a la derecha, **Review changes**:
   - **Approve:** todo bien.
   - **Request changes:** falta algo, y explicas qué.

## Reglas que no se rompen

- **Nunca** se sube directo a `main` ni a `develop`. GitHub lo bloquea.
- Una tarjeta, una rama.
- Los PR van **hacia `develop`**. Solo Walter o Rolando pasan `develop` a `main`.
- No subas contraseñas, llaves ni datos reales: los repos son públicos.
- Las migraciones de la base de datos las crea **solo Diana**, para evitar conflictos.

## Dónde van las contraseñas y llaves

Los repos son públicos, así que **nada secreto se sube a GitHub**: contraseñas de la base de datos, llaves de AWS, el secreto del JWT, tokens.

- **En tu computadora:** van en un archivo `.env` (en Android, en `local.properties`). Ese archivo **no se sube**: ya está ignorado por el `.gitignore` del repo. Comprueba con `git status` que no aparezca antes de hacer commit.
- **En el repo:** solo se sube `.env.example`, con los nombres de las variables y valores falsos, para que los demás sepan qué llenar. Ejemplo:
  ```
  DB_HOST=localhost
  DB_USER=usuario
  DB_PASSWORD=cambia-esto
  JWT_SECRET=cambia-esto
  ```
- **Para usarlo:** copia `.env.example` a `.env` y pon tus valores reales.
- **En la nube (AWS):** las variables y secretos se configuran en el servicio donde corre la API, nunca dentro del código ni de la imagen de Docker.
- **Las contraseñas reales** se las pasan entre ustedes por un canal privado, no por el grupo ni por un commit.

**Si subes una contraseña por error:** avisa de inmediato y **cámbiala**. Borrarla del código no basta, porque queda guardada en el historial de GitHub y cualquiera la puede ver.

## Problemas comunes

- **"No me deja hacer push a develop":** es normal. Sube tu rama `feature/...` y abre un PR.
- **Me equivoqué de rama:** avisa antes de seguir, es fácil de arreglar.
- **Conflicto al unir:** alguien cambió lo mismo que tú. Trae lo último con `git pull origin develop` en tu rama, resuelve el conflicto y vuelve a subir. Si no sabes cómo, pide ayuda a un compañero.
- **No me llega la invitación a la organización:** entra a `https://github.com/orgs/OVIUM-team/invitation`.
