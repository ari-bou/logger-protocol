# Logger Protocol

This package provides a common interface for logging utilities. `LoggerProtocol` is a protocol class that conforms to the `Logger` class implemented in the standard Python `logging` module. The main use case for this protocol class is when library authors need to support custom logging plugins.

```python
import logging

from logger_protocol import LoggerProtocol


class MyClass:
    _logger: Logger Protocol

    def __init__(self, logger: LoggerProtocol | None = None):
        self._logger = logger or logging.getLogger(__name__)
```

## Explicit Subclasses

### SilentLogger

The `SilentLogger` is a stateless type that implements the `LoggerProtocol` by way of static methods. Each of these methods no-ops upon invocation, resulting in no logs being produced. This is particularly useful when library authors need to support disabling of all logs produced by a given facility. 

```python
import logging

from logger_protocol import LoggerProtocol, SilentLogger


class MyClass:
    _logger: LoggerProtocol

    def __init__(self, verbose: bool = True):
        self._logger = logging.getLogger(__name__) if verbose else SilentLogger
```