Cache Module
============

.. automodule:: tradebot.core.cache
   :members:
   :undoc-members:
   :show-inheritance:

Overview
--------

The cache module provides Redis-based caching functionality for the trading bot.
It handles caching of market data, orders, positions and other trading-related information.

Key Components
--------------

- RedisCache: Main cache implementation using Redis
- CacheKey: Enum of cache key types
- CacheManager: High-level cache management interface

Usage Example
-------------

.. code-block:: python

   from tradebot.core.cache import RedisCache
   
   # Initialize cache
   cache = RedisCache()
   
   # Cache market data
   await cache.set_market_data("BTCUSDT", data)
   
   # Get cached data
   data = await cache.get_market_data("BTCUSDT")

AsyncCache
---------

.. py:class:: AsyncCache(strategy_id: str, user_id: str, task_manager: TaskManager, sync_interval: int = 60, expire_time: int = 3600)

   Cache system for storing order and position data with Redis persistence.

   :param str strategy_id: Strategy identifier
   :param str user_id: User identifier 
   :param TaskManager task_manager: Task manager for async operations
   :param int sync_interval: Interval in seconds for syncing to Redis
   :param int expire_time: Time in seconds before data expires

   .. py:method:: apply_position(order: Order)
      :async:

      Update position based on order execution.

      :param Order order: Order that affects position

   .. py:method:: get_position(symbol: str) -> Position
      :async:

      Get current position for a symbol.

      :param str symbol: Trading pair symbol
      :return: Position object if exists, else None
      :rtype: Optional[Position]

   .. py:method:: order_initialized(order: Order)

      Initialize a new order in the cache.

      :param Order order: New order to track

   .. py:method:: order_status_update(order: Order)

      Update status of existing order.

      :param Order order: Order with updated status

   .. py:method:: get_order(order_id: str) -> Order
      :async:

      Get order by ID.

      :param str order_id: Order identifier
      :return: Order object if exists, else None
      :rtype: Optional[Order]

   .. py:method:: get_symbol_orders(symbol: str, in_mem: bool = True) -> Set[str]
      :async:

      Get all order IDs for a symbol.

      :param str symbol: Trading pair symbol
      :param bool in_mem: Whether to only check in-memory cache
      :return: Set of order IDs
      :rtype: Set[str]

   .. py:method:: get_open_orders(symbol: str = None, exchange: ExchangeType = None) -> Set[str]
      :async:

      Get open order IDs filtered by symbol or exchange.

      :param Optional[str] symbol: Trading pair symbol filter
      :param Optional[ExchangeType] exchange: Exchange filter
      :return: Set of open order IDs
      :rtype: Set[str]

   .. py:method:: start()
      :async:

      Start the cache system.
      
      - Initializes Redis connection
      - Starts periodic sync task

   .. py:method:: close() 
      :async:

      Close the cache system.
      
      - Syncs final state to Redis
      - Closes Redis connection
