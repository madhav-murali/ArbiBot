# Crypto Arbitrage Trading Bot

A sophisticated, production-ready arbitrage trading bot that monitors price spreads across centralized exchanges (Binance, Bybit) and decentralized exchanges (dYdX, Reya) to execute delta-neutral profit strategies.

## Features

### Core Functionality
- **Real-time arbitrage detection** across CEX and DEX perpetual futures markets
- **Delta-neutral trading** with simultaneous long/short positions
- **Intelligent risk management** with dynamic entry/exit thresholds
- **Precise decimal arithmetic** for accurate profit calculations
- **Robust error handling** and execution failure recovery

### Advanced Trading Logic
- Dynamic spread thresholds accounting for:
  - Funding rates and borrowing costs
  - Trading commissions and slippage
  - Market liquidity conditions
  - Volatility filtering
- Configurable exit strategies:
  - Target spread achievement
  - Position timeout management
  - Stop-loss protection
  - Adverse movement detection

### Risk Management
- Position sizing based on account balance and risk tolerance
- Liquidity validation before trade execution
- Volatility filtering to avoid unstable markets
- Maximum concurrent position limits
- Funding rate monitoring

### Monitoring & Analytics
- Real-time dashboard with position tracking
- Comprehensive logging with trade history
- Backtesting engine for strategy validation
- Performance metrics and P&L tracking
- Configurable alerts and notifications

## Installation

### Prerequisites
- Python 3.9 or higher
- Git

### Setup
```bash
# Clone the repository
git clone <repository-url>
cd crypto-arbitrage-bot

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Copy configuration template
cp arbitrage_config.json.example arbitrage_config.json
```

## Configuration

### Exchange API Setup

1. **Binance**
   - Create API key at https://www.binance.com/en/my/settings/api-management
   - Enable futures trading permissions
   - Add API key and secret to config file

2. **Bybit**
   - Create API key at https://www.bybit.com/app/user/api-management
   - Enable derivatives trading permissions
   - Add API key and secret to config file

3. **dYdX**
   - Create account at https://trade.dydx.exchange/
   - Generate API key and stark private key
   - Add credentials to config file

### Configuration Parameters

Edit `arbitrage_config.json`:

```json
{
  "trading": {
    "min_entry_spread_bps": 15,     // Minimum spread to enter (basis points)
    "target_exit_spread_bps": 5,    // Target spread to exit
    "stop_loss_spread_bps": -30,    // Stop loss threshold
    "max_position_usd": 1000,       // Maximum position size
    "leverage": 3,                  // Leverage multiplier
    "risk_per_trade": 0.02,         // Risk per trade (2%)
    "position_timeout_seconds": 300  // Position timeout (5 minutes)
  }
}
```

## Usage

### Basic Operation
```bash
# Run the bot with default settings
python arbitrage_bot.py

# Run with monitoring dashboard
python arbitrage_bot.py --monitor

# Run with custom configuration
python arbitrage_bot.py --config my_config.json

# Dry run (no actual trades)
python arbitrage_bot.py --dry-run
```

### Backtesting
```bash
# Run backtest on historical data
python arbitrage_bot.py --backtest historical_data.json
```

### Advanced Usage
```python
from arbitrage_bot import ArbitrageEngine, TradingConfig

# Create custom configuration
config = TradingConfig()
config.min_entry_spread = Decimal('20')  # 20 bps minimum
config.max_position_usd = Decimal('5000')

# Initialize and run engine
engine = ArbitrageEngine(config)
await engine.start()
```

## Strategy Logic

### Arbitrage Detection
1. **Price Monitoring**: Continuously fetch orderbook data from all exchanges
2. **Spread Calculation**: Calculate price differences between exchanges
3. **Opportunity Validation**: Filter opportunities by:
   - Minimum spread threshold
   - Liquidity requirements
   - Volatility conditions
   - Funding rate constraints

### Trade Execution
1. **Position Sizing**: Calculate optimal position size based on:
   - Account balance and risk limits
   - Available liquidity
   - Spread magnitude
2. **Simultaneous Execution**: Place long and short orders simultaneously
3. **Execution Monitoring**: Handle partial fills and execution failures

### Risk Management
1. **Entry Validation**:
   - Minimum spread requirements
   - Liquidity checks
   - Volatility filtering
   - Funding rate validation

2. **Position Management**:
   - Target profit monitoring
   - Stop-loss protection
   - Position timeout handling
   - Adverse movement detection

3. **Exit Logic**:
   - Spread convergence to target
   - Time-based exits
   - Risk-based exits
   - Emergency liquidation

## Performance Optimization

### Latency Reduction
- Async/await architecture for concurrent operations
- WebSocket connections for real-time data
- Connection pooling and reuse
- Optimized order placement logic

### Accuracy Improvements
- Decimal arithmetic for precise calculations
- Real-time funding rate monitoring
- Dynamic slippage estimation
- Liquidity-aware position sizing

## Monitoring

### Dashboard Features
- Exchange connection status
- Active position tracking
- Real-time P&L monitoring
- Opportunity detection metrics
- Performance statistics

### Logging
- Structured logging with multiple levels
- Trade execution history
- Error tracking and debugging
- Performance metrics logging

## Safety Features

### Execution Safety
- Atomic trade execution with rollback
- Partial fill handling
- Connection failure recovery
- Rate limit management

### Risk Controls
- Maximum position limits
- Drawdown protection
- Volatility circuit breakers
- Emergency shutdown procedures

## Troubleshooting

### Common Issues

1. **Connection Failures**
   ```
   Error: Failed to connect to exchange
   Solution: Check API credentials and network connectivity
   ```

2. **Insufficient Balance**
   ```
   Error: Insufficient margin balance
   Solution: Reduce position size or add funds
   ```

3. **API Rate Limits**
   ```
   Error: Rate limit exceeded
   Solution: Reduce request frequency or upgrade API tier
   ```

### Debug Mode
```bash
# Enable debug logging
python arbitrage_bot.py --log-level DEBUG

# Save detailed logs
python arbitrage_bot.py --log-file debug.log
```

## Development

### Testing
```bash
# Run unit tests
pytest tests/

# Run integration tests
pytest tests/integration/

# Run with coverage
pytest --cov=arbitrage_bot tests/
```

### Contributing
1. Fork the repository
2. Create feature branch (`git checkout -b feature/new-feature`)
3. Commit changes (`git commit -am 'Add new feature'`)
4. Push to branch (`git push origin feature/new-feature`)
5. Create Pull Request

## Disclaimer

This trading bot is for educational and research purposes. Cryptocurrency trading involves substantial risk of loss. Users should:

- Thoroughly test with paper trading before live deployment
- Start with small position sizes
- Monitor performance closely
- Understand the risks involved
- Comply with local regulations

The authors are not responsible for any financial losses incurred through the use of this software.

## License

MIT License - see LICENSE file for details

## Support

For questions and support:
- Create an issue on GitHub
- Check the documentation
- Review existing issues and discussions