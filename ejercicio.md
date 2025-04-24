# 🧠 Ejercicio: Chat WebSocket con expulsión automática

## Enunciado

Crea un componente `ChatRoom` que se conecte a un servidor WebSocket.

### Objetivos:

- Mostrar y enviar mensajes.
- Detectar si el mensaje es `"expulsion"` y desconectar al usuario.
- Tipar mensajes con `MensajeChat`.

---

## 🗂 Estructura de Archivos

```bash
src/
├── components/
│   └── ChatRoom.tsx
├── pages/
│   └── ChatPage.tsx
├── types/
│   └── MensajeChat.ts
├── utils/
│   └── mockSocket.ts
```

# Mock socket

    - mock-socket se utiliza para pruebas en entorno local cuando:
    - No tienes un backend listo.
    - Quieres simular respuestas del servidor WebSocket.

  
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



## 🛑 Limitaciones

- **No se usa en producción**.
- No soporta todo el protocolo WebSocket, solo lo necesario para simularlo.
- Es útil solo en el entorno del navegador (no en apps móviles o servidores reales).

---

## Conclusión

> Usa `mock-socket` para desarrollar y hacer pruebas rápidas sin backend.  
> Cuando tu app esté lista para producción, cambia a `WebSocket` real con un servidor real (Node.js, Python, etc.).

---