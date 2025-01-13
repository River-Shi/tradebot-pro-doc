Logging Module
=============

.. automodule:: tradebot.core.log
   :members:
   :undoc-members:
   :show-inheritance:

Overview
--------

The logging module provides structured logging functionality for the trading bot.
It includes formatters and handlers for both console and file logging.

Key Components
-------------

- setup_logging: Function to initialize logging configuration
- LogFormatter: Custom formatter for structured log output
- LogHandler: Custom handler for log routing

Usage Example
------------

.. code-block:: python

   from tradebot.core.log import setup_logging
   
   # Initialize logging
   setup_logging(
       log_level="INFO",
       log_file="trading.log"
   )
   
   # Use logger
   logger = logging.getLogger(__name__)
   logger.info("Trading started", extra={
       "exchange": "binance",
       "symbol": "BTCUSDT"
   }) 

SpdLog
------

.. py:class:: SpdLog

   Structured logging system with file rotation.

   .. py:classmethod:: get_logger(name: str, level: Literal["DEBUG", "INFO", "WARNING", "ERROR", "CRITICAL"] = "INFO", flush: bool = False) -> spd.Logger

      Get or create a logger instance.

      :param str name: Logger name
      :param str level: Log level
      :param bool flush: Auto-flush after each log
      :return: Logger instance
      :rtype: spdlog.Logger

   .. py:classmethod:: initialize(log_dir: str = ".logs", async_mode: bool = True, setup_error_handlers: bool = True)

      Initialize the logging system.

      :param str log_dir: Directory for log files
      :param bool async_mode: Enable async logging
      :param bool setup_error_handlers: Setup global error handlers

   .. py:classmethod:: close_all_loggers()

      Close all logger instances and release resources.
