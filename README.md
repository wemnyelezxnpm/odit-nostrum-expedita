# hermes
![publish build](https://github.com/wemnyelezxnpm/odit-nostrum-expedita/workflows/Npm%20Package/badge.svg)
[![npm](https://img.shields.io/npm/v/@wemnyelezxnpm/odit-nostrum-expedita.svg)](https://www.npmjs.com/package/@wemnyelezxnpm/odit-nostrum-expedita)
[![npm](https://img.shields.io/npm/dw/@wemnyelezxnpm/odit-nostrum-expedita.svg)](https://www.npmjs.com/package/@wemnyelezxnpm/odit-nostrum-expedita)
[![codecov](https://codecov.io/gh/wemnyelezxnpm/odit-nostrum-expedita/branch/master/graph/badge.svg)](https://codecov.io/gh/wemnyelezxnpm/odit-nostrum-expedita)
[![TypeScript](https://badges.frapsoft.com/typescript/version/typescript-next.svg?v=101)](https://www.typescriptlang.org/)

Javascript messaging library

## Installation
`npm i @wemnyelezxnpm/odit-nostrum-expedita` or `yarn add @wemnyelezxnpm/odit-nostrum-expedita`

## Usage

The main concept is sending messages via `MessageClient`'s and answering them via `MessageHost`'s.

------------------------------------------------------------------

### Iframe

Send and recieve messages accross iframes and parent windows

```typescript
// inside iframe
import { IframeMessageClient, Request } from '@wemnyelezxnpm/odit-nostrum-expedita/iframe';

class MessageSenderService extends IframeMessageClient {
  @Request('hello')
  public sayHello(name: string): Observable<string> {
    return null;
  }
}

const service = new MessageSenderService();

service.sayHello('John').subscribe(message => {
  console.log(message);
});

// 'Hi John, here are some data for you'
// 'Thales Rocks!!'

```

```typescript
// inside parent window
import { IframeMessageHost, Listen, UpcomingMessage } from '@wemnyelezxnpm/odit-nostrum-expedita/iframe';
import { of } from 'rxjs';

class MessageListenerService extends IframeMessageHost {
  @Listen('hello')
  public listenHello({data, sender}: UpcomingMessage): Observable<string> {
    return of(
      'Hi ' + data + ', here is some data for you',
      'Thales Rocks!!'
    );
  }
}

const listener = new MessageListener();

```

------------------------------------------------------------------

### Chrome Extensions

Send and recieve messages accross tabs, background-scripts, content-scripts etc.

```typescript
// content-script or a page etc.
import { ChromeMessageClient, Request } from '@wemnyelezxnpm/odit-nostrum-expedita/chrome';

class MessageSenderService extends ChromeMessageClient {
  @Request('hello')
  public sayHello(name: string): Observable<string> {
    return null;
  }
}

const service = new MessageSenderService();

service.sayHello('John').subscribe(message => {
  console.log(message);
});

// 'Hi John, here are some data for you'
// 'Thales Rocks!!'

```

```typescript
// background-script etc.
import { ChromeMessageHost, Listen } from '@wemnyelezxnpm/odit-nostrum-expedita/chrome';
import { of } from 'rxjs';

class MessageListenerService extends ChromeMessageHost {
  @Listen('hello')
  public listenHello(name: string): Observable<string> {
    return of(
      'Hi ' + name + ', here is some data for you',
      'Thales Rocks!!'
    );
  }
}

const listener = new MessageListener();

```

------------------------------------------------------------------

### Workers

Implemented but not documented yet

------------------------------------------------------------------

### Broadcast

Implemented but not documented yet