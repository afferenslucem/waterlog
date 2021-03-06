# Waterlog

Easy logging utils

## Menu

* [Technologies](#technologies)
* [Examples](#examples)
* [Setup](#setup)

## Technologies

Project is created with:

* typescript 3.9.7
* chai 4.2.0
* mocha 8.1.0
* ts-mocha 7.0.0
* sinon 9.0.2
* moment 2.27.0

## Examples

### Basic usage

```typescript
import {ConsoleLoggerFactory, LogLevel} from 'waterlog';

const factory = new ConsoleLoggerFactory([
    { // Simple configuration
        name: 'logger',
        logger: LogLevel.Info
    },
    { // Configuration with namespace
        name: {
            namespace: 'namespace',
            loggerName: 'logger'
        },
        logger: LogLevel.Info
    },
    { // Configuration with only namespace
        name: {
            namespace: 'namespace2',
        },
        logger: LogLevel.Info
    }
]);

// Getting logger for namespace
const namespacedLogger = factory.getLogger({
    namespace: 'namespace2',
    loggerName: 'funnyLogger'
});
namespacedLogger.info('info message'); // 2020-08-06 13:45:54.600 namespace2.funnyLogger - INFO - info message

// Getting logger by name
const logger = factory.getLogger('logger');
logger.info('info message'); // 2020-08-06 13:45:54.600 logger - INFO - info message

// Getting logger by namespace and name
const fullnamedLogger = factory.getLogger({
    namespace: 'namespace',
    loggerName: 'logger'
});

fullnamedLogger.info('info message'); //2020-08-06 13:45:54.606 namespace.logger - INFO - info message


// Getting undefined logger
const defaultLogger = factory.getLogger('undefinedLogger');

defaultLogger.info('info message'); // Will not show info data at console
defaultLogger.warn('warn message'); // 2020-08-06 13:45:54.626 undefinedLogger - WARN - warn message
```

> [!WARNING]
> Default logger log level is warning

### Override default logger log level

```typescript
import {ConsoleLoggerFactory, LogLevel} from 'waterlog';

const factory = new ConsoleLoggerFactory([
    { // Overriding configuration
        name: 'default',
        logger: LogLevel.All
    }
]);

const defaultLogger = factory.getLogger('undefinedLogger');

defaultLogger.debug('debug message'); // 2020-08-06 13:55:01.484 undefinedLogger - DEBUG - debug message
defaultLogger.info('info message'); // 2020-08-06 13:55:01.484 undefinedLogger - INFO - info message
```

## Setup

To use this project, install it locally using npm:

`$npm i waterlog`
