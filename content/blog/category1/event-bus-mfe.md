---
title: Event Bus (for micro-frontend)
date: 2023-10-25 18:10:71
category: category1
thumbnail: { thumbnailSrc }
draft: false
---

## Quick note

### type-safe CustomEvent

`event as CustomEvent<EventDetail>`

```ts
const windowEventListener = (event: Event) => {
  const { appId, eventName: eventKey, eventData } = (event as CustomEvent<
    EventDetail
  >).detail

  if (appId === this.appId) return

  if (eventKey === eventName) {
    callback(eventData)
  }
}

window.addEventListener(EVENT_CHANNEL_NAME, windowEventListener)
```

`declare global { interface WindowEventMap {} }`

```tsx
export const CurrentUserProvider = ({ children }: CurrentUserProviderProps) => {
  useEffect(() => {
    const fetcher = async () => {
      try {
        const myInfo = await fetchMyInfo()
        setCurrentUser({ isLoggedIn: true, isLoading: false, ...myInfo })
      } catch {
        setCurrentUser({ isLoggedIn: false, isLoading: false })
      }
    }

    const handler = (
      event: CustomEvent<{ appId: string; eventName: string }>
    ) => {
      if (event.detail.appId === 'career-app-root') return
      if (event.detail.eventName !== 'toggleJobPositionSuggestion') return

      fetcher()
    }

    window.addEventListener('event-bus', handler)

    return () => {
      window.removeEventListener('event-bus', handler)
    }
  }, [])

  return (
    <CurrentUserContext.Provider value={[currentUser, setCurrentUser]}>
      {children}
    </CurrentUserContext.Provider>
  )
}

export default CurrentUserProvider

declare global {
  interface WindowEventMap {
    'event-bus': CustomEvent<{
      appId: string
      eventName: string
    }>
  }
}
```

## 📚 함께 읽기

- event bus
  - [Oskari - How to Easily Create an Event Bus for a Micro Frontend](https://oskari.io/blog/event-bus-micro-frontend)
  - [github - micro-front-end-demo -pubsub.ts](https://github.com/rautio/micro-frontend-demo/blob/main/main/src/services/pubsub.ts)
  - [npm - @zenstack/zen-bus](https://npm.io/package/@zenstack/zen-bus)
  - [medium - Building an Event-Driven Microservice in Node.js: A Basic Example](https://medium.com/@nathanbyers13/building-an-event-driven-microservice-in-node-js-a-basic-example-c2c31d9f137c)
  - [CSS-TRICKS - Let’s Create a Lightweight Native Event Bus in JavaScript ](https://css-tricks.com/lets-create-a-lightweight-native-event-bus-in-javascript/): 주석 DOM Node(`new Comment()`)를 사용해서 이벤트 버스를 만드는 방법
- type-safe CustomEvent
  - [tutorials point - How to fix property not existing on EventTarget in TypeScript?](https://www.tutorialspoint.com/how-to-fix-property-not-existing-on-eventtarget-in-typescript)
  - [divotion - Creating type-safe events in Typescript](https://www.divotion.com/blog/creating-type-safe-events)
  - [medium - Typesafe CustomEvents on your Frontend](https://medium.com/scout24-engineering/typesafe-customevents-on-your-frontend-b3265aff6cf0): `declare global`
