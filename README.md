# Características del ejercicio

## `mock-socket` vs `WebSocket` en React

| Característica                           | `WebSocket` (nativo)                | `mock-socket`                       |
|------------------------------------------|-------------------------------------|-------------------------------------|
| ¿Está en producción?                     | ✅ Sí                               | ❌ No (solo desarrollo / testing)   |
| ¿Simula un servidor WebSocket?           | ❌ No                               | ✅ Sí                               |
| ¿Permite pruebas sin servidor real?      | ❌ No                               | ✅ Sí                               |
| ¿Compatible con navegador real?          | ✅ Sí                               | ✅ Sí (solo entorno de desarrollo)  |
| ¿Compatible con React?                   | ✅ Sí                               | ✅ Sí                               |
| ¿Puedes interceptar y modificar mensajes?| ❌ Difícil                          | ✅ Muy fácil                         |
| ¿Requiere backend real?                  | ✅ Sí                               | ❌ No                               |

---

## `mock-socket` se utiliza para ** pruebas en entorno local** cuando:

- No tienes un backend listo.
- Quieres simular respuestas del servidor WebSocket.
- Estás enseñando cómo funciona WebSocket en el frontend.

---

## 🛑 Limitaciones

- **No se usa en producción**.
- No soporta todo el protocolo WebSocket, solo lo necesario para simularlo.
- Es útil solo en el entorno del navegador (no en apps móviles o servidores reales).

---

## Conclusión

> Usa `mock-socket` para desarrollar y hacer pruebas rápidas sin backend.  
> Cuando tu app esté lista para producción, cambia a `WebSocket` real con un servidor real (Node.js, Python, etc.).

---

## Cambiar `mock-socket` a un **WebSocket real en producción**, conservando tu estructura en React.

---

## 🏗️ Paso 1: Usar `WebSocket` nativo en lugar de `mock-socket`

### 🔄 Antes (`mock-socket.ts` activado en desarrollo)

```ts
// src/utils/mockSocket.ts
import { Server } from 'mock-socket';

const mockServer = new Server('ws://localhost:1234');
// ...
```

Y en tu componente:

```tsx
import '../utils/mockSocket'; // Se importa para activar el servidor simulado
```

---

## ✅ Después: usar WebSocket real

### 1. ❌ Elimina la línea:
```tsx
import '../utils/mockSocket';
```

### 2. ✅ Usa el WebSocket de producción:

```tsx
ws.current = new WebSocket('wss://tuserver.com/chat'); // ejemplo real
```

📌 Reemplaza `wss://tuserver.com/chat` con la URL de tu backend WebSocket (nota que `wss://` es para WebSocket seguro, como HTTPS).

---

## 🧠 Tip: Alternar entre mock y real fácilmente

Puedes usar una condición como esta:

```tsx
const socketURL = import.meta.env.MODE === 'development'
  ? 'ws://localhost:1234'
  : 'wss://tuserver.com/chat';

ws.current = new WebSocket(socketURL);
```

> Esto usará `mock-socket` en desarrollo y `WebSocket` real en producción.

---

## 🎯 Servidor WebSocket real (ejemplo básico en Node.js)

Si quieres probar un servidor real, puedes usar este ejemplo con `ws`:

```bash
npm install ws
```

```js
// server.js
const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 1234 });

wss.on('connection', ws => {
  ws.on('message', message => {
    const data = JSON.parse(message);

    if (data.contenido === 'expulsion') {
      ws.send(JSON.stringify({ tipo: 'expulsion' }));
      ws.close();
    } else {
      ws.send(JSON.stringify({ tipo: 'mensaje', ...data }));
    }
  });
});
```

---
