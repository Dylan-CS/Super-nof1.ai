# Super NOF1.ai - AI-Powered Cryptocurrency Trading System

Inspired by Alpha Arena and Open-NOF1.ai projects, this project builds upon Open-NOF1.ai with comprehensive improvements including enhanced prompts, data acquisition, feedback logic, optimized UI pages, and chart displays. A sophisticated AI-driven automated cryptocurrency futures trading system built with Next.js, integrating Binance Futures API and DeepSeek AI models.

## Latest Updates

**November 3, 2025**
- Fixed frontend display issues with insufficient decimal precision in trades
- Modified chat output to display single messages instead of five, saving space

**Update Instructions:**
- Copy these files to overwrite existing ones:
  - `lib/ai/run.ts`
  - `prisma/schema.prisma`
  - `components/models_view.tsx`
  - `app/api/cron/3-minutes-run-interval/route.ts`
  - `cron.ts`
- Update database by running:
  ```bash
  npx prisma db push
  npx prisma generate
  ```
- Run `npm run dev` to start using the updated system

## Trading Pipeline

The trading logic follows this workflow:
1. Fetch real-time market data from official Binance API
2. Every 3 minutes, call DeepSeek LLM API
3. AI model analyzes market data using carefully crafted prompts
4. Execute trading strategies via exchange API

## Core Features

### 🤖 AI Trading Decisions
- **Multi-Model Support**: Integrated DeepSeek Chat models for market analysis
- **Technical Indicators**: Comprehensive analysis using RSI, MACD, EMA, volume metrics
- **Risk Management**: Automated stop-loss, take-profit, dynamic leverage adjustment
- **Learning Feedback**: Continuous strategy optimization from historical trade analysis

### 💼 Trading Capabilities
- **Automated Trading**: Multi-currency support (BTC, ETH, SOL, BNB, DOGE, ADA, DOT, MATIC, AVAX, LINK)
- **Stop-Loss/Take-Profit**: Automated order management and position protection
- **Position Management**: Real-time monitoring of holdings and P&L
- **Risk Control**: Multi-layered risk protection mechanisms

### 📊 Data Visualization
- **Real-time Charts**: Key metrics including account balance, ROI, performance
- **Trade History**: Complete transaction records with AI decision logs
- **Performance Analytics**: Win rate, average P&L, maximum drawdown statistics

### 🔒 Security Features
- **Virtual Trading**: Testnet support for strategy validation (demo-fapi.binance.com)
- **Live Trading**: Seamless transition to real trading mode
- **API Key Encryption**: Secure environment variable management
- **Proxy Support**: Proxy configuration for Binance API access

---

## System Requirements

### Required Software
- **Node.js** 18.0 or higher
- **npm** or **yarn** package manager
- **PostgreSQL** 14.0 or higher
- **Git** (for cloning the repository)

### Optional Software
- **Proxy Tools** (Clash, V2Ray) for accessing Binance API
- **VSCode** or other code editor

### Account Requirements
- **Binance Account**: Registered account with API key creation
- **DeepSeek API Key**: Required for AI functionality (OpenRouter available as alternative)

---

## Complete Installation Guide

### Step 1: Install Node.js

#### Windows Users:
1. Visit [Node.js Official Website](https://nodejs.org/)
2. Download LTS version (recommended 18.x or higher)
3. Run installer with default options
4. Verify installation:
```bash
node --version
npm --version
```

#### macOS Users:
Using Homebrew:
```bash
brew install node@18
```

#### Linux Users:
```bash
# Ubuntu/Debian
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# Verify installation
node --version
npm --version
```

### Step 2: Install PostgreSQL Database

#### Windows Users:
1. **Download Installer**
   - Visit [PostgreSQL Official Website](https://www.postgresql.org/download/windows/)
   - Download latest version (14.x or higher)

2. **Run Installer**
   - Double-click installer file
   - Choose installation path (default recommended)
   - Set superuser (postgres) password ***(Remember this password!)***
   - Use default port 5432
   - Select default locale

3. **Verify Installation**
   ```bash
   psql --version
   ```

4. **Configure Environment Variables** (if psql command not found)
   - Right-click "This PC" → Properties → Advanced System Settings → Environment Variables
   - Add to System Path: `C:\Program Files\PostgreSQL\14\bin`

#### macOS Users:
1. **Install via Homebrew**
   ```bash
   brew install postgresql@14
   brew services start postgresql@14
   ```

2. **Verify Installation**
   ```bash
   psql --version
   ```

#### Linux Users:
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install postgresql postgresql-contrib

# Start service
sudo systemctl start postgresql
sudo systemctl enable postgresql

# Verify installation
psql --version
```

### Step 3: Create Database

1. **Connect to PostgreSQL**

   **Windows:**
   ```bash
   psql -U postgres
   # Enter password set during installation
   ```

   **macOS/Linux:**
   ```bash
   sudo -u postgres psql
   ```

2. **Create Database and User**
   ```sql
   -- Create database
   CREATE DATABASE nof1;

   -- Create user (optional, recommended)
   CREATE USER trading_user WITH PASSWORD 'your_secure_password';

   -- Grant privileges
   GRANT ALL PRIVILEGES ON DATABASE nof1 TO trading_user;

   -- Exit psql
   \q
   ```

3. **Record Database Connection Information**
   - Database Name: `nof1`
   - Username: `trading_user` (or `postgres`)
   - Password: Your set password
   - Host: `localhost`
   - Port: `5432`

### Step 4: Obtain Binance API Keys

#### Testnet (Recommended for Beginners):
1. Visit [Binance Testnet](https://testnet.binancefuture.com/)
2. Login with GitHub account
3. Click profile icon → API Key
4. Create new API Key
5. Save API Key and Secret Key

#### Live Trading:
⚠️ **Warning: Live trading involves real funds, proceed with caution!**

1. Login to [Binance Official Website](https://www.binance.com/)
2. Account → API Management
3. Create API Key
4. **Important: Configure API Permissions** (required to avoid errors)
   - ✅ Enable Spot & Margin Trading
   - ✅ Enable Futures Trading
   - ✅ Enable Read Permissions
5. **Configure IP Whitelist** (required for trading)
6. Save API Key and Secret Key

### Step 5: Obtain AI API Keys (Optional)

#### Option A: DeepSeek (Recommended)
1. Visit [DeepSeek Platform](https://platform.deepseek.com/)
2. Register account and login
3. Navigate to API Keys page
4. Create new API Key
5. Save API Key

#### Option B: OpenRouter (Alternative)
1. Visit [OpenRouter](https://openrouter.ai/)
2. Register account and login
3. Create API Key
4. Save API Key

### Step 6: Clone Project

```bash
# Clone repository
git clone git@github.com:qingshungLI/Super-nof1.ai.git

# Enter project directory
cd Super-nof1.ai
```

### Step 7: Install Project Dependencies

```bash
# Using npm
npm install

# Or using yarn
yarn install

# Or using pnpm (recommended, faster)
npm install -g pnpm
pnpm install
```

**Installation Time**: 5-15 minutes depending on network speed

**If experiencing network issues**:
```bash
# Use Chinese mirror
npm config set registry https://registry.npmmirror.com
npm install
```

### Step 8: Configure Environment Variables

1. **Copy Environment Template**
   ```bash
   # Windows
   copy .env.example .env

   # macOS/Linux
   cp .env.example .env
   ```

2. **Edit `.env` File**

   Open `.env` file with any text editor and configure the following:

   ```env
   # ==========================================
   # Database Configuration
   # ==========================================
   # Format: postgresql://username:password@host:port/database_name
   DATABASE_URL="postgresql://trading_user:your_secure_password@localhost:5432/nof1"
   # Replace 'your_secure_password' with your actual password (remove parentheses)
   # Replace 'nof1' with your actual database name if different

   # Proxy Configuration (Required for Mainland China access)
   # ==========================================
   # If accessing Binance API through proxy (Clash port 7890, V2Ray port 10809)
   BINANCE_HTTP_PROXY="http://127.0.0.1:7890"
   # If no proxy needed, set to true
   # BINANCE_DISABLE_PROXY=true

   # ==========================================
   # Binance API Configuration (Important Update!)
   # ==========================================

   # Testnet API Configuration
   BINANCE_TESTNET_API_KEY="your-testnet-api-key"
   BINANCE_TESTNET_API_SECRET="your-testnet-api-secret"
   BINANCE_TESTNET_BASE_URL="https://demo-fapi.binance.com"
   # Keep quotes around API keys!

   # Live Trading API Configuration
   BINANCE_LIVE_API_KEY="your-live-api-key"
   BINANCE_LIVE_API_SECRET="your-live-api-secret"
   BINANCE_LIVE_BASE_URL="https://fapi.binance.com"

   # Request timeout (recommended to keep as tested)
   BINANCE_FETCH_TIMEOUT_MS="25000"

   # Trading Mode: dry-run (testnet) or live (real trading)
   # 💡 Just modify this single parameter to switch modes! System auto-detects API config
   TRADING_MODE="dry-run"
   # Change to "live" for real trading

   # Risk Control Parameters (Applies to both virtual and live trading)
   MAX_POSITION_SIZE_USDT=5000  # Maximum position size in USDT
   MAX_LEVERAGE=30  # Maximum allowed leverage (30x for high-yield strategy)
   DAILY_LOSS_LIMIT_PERCENT=20  # Daily loss limit as percentage of capital

   # ==========================================
   # AI Model Configuration
   # ==========================================
   # DeepSeek API Key (Recommended)
   DEEPSEEK_API_KEY="your-deepseek-api-key"

   # ==========================================
   # Application Configuration (Required)
   # ==========================================
   NEXT_PUBLIC_URL="http://localhost:3000"
   CRON_SECRET_KEY="secretkey_change_this_in_production"
   ```

### Step 9: Initialize Database

```bash
# Generate Prisma client
npx prisma generate

# Create database tables
npx prisma db push
```

**If encountering database connection errors**:
- Verify DATABASE_URL is correct
- Confirm PostgreSQL service is running
- Validate database password and name are correct

### Step 10: Start Project

```bash
# Start in development mode
npm run dev

# Or using yarn
yarn dev

# Or using pnpm
pnpm dev
```

**After successful startup**:
- Access http://localhost:3000 to view frontend interface
- System automatically starts AI trading decisions (every 3 minutes)
- Logs will display: `🎮 Trading Mode: DRY-RUN (Virtual Trading)`

**To switch between testnet and live trading**:
- Configure both API sets in .env
- Simply toggle TRADING_MODE between "live" and "dry-run"

---

## Database Management

Use pgAdmin for visual database management:

![Database Dashboard](https://github.com/user-attachments/assets/1ec01f5d-ddc5-4922-911a-5981a02c7acb)

View data fluctuations in the dashboard and use SQL queries for analysis.

## 📊 Database Schema Details

### Chat Table (AI Decision Records)
```prisma
model Chat {
  id          String    @id @default(cuid())
  model       String    // AI model name
  chat        String    @db.Text  // AI analysis content
  reasoning   String?   @db.Text  // Reasoning process
  userPrompt  String    @db.Text  // User prompt
  tradings    Trading[] // Associated trades
  createdAt   DateTime  @default(now())
  updatedAt   DateTime  @updatedAt
}
```

### Trading Table (Transaction Records)
```prisma
model Trading {
  id              String    @id @default(cuid())
  symbol          String    // Trading pair, e.g., BTC
  operation       String    // Operation: Buy/Sell/Hold
  pricing         Float?    // Price
  amount          Float?    // Quantity
  leverage        Int?      // Leverage multiplier
  stopLossPercent Float?    // Stop loss percentage
  takeProfitPercent Float?  // Take profit percentage
  orderId         String?   // Order ID
  status          String    @default("pending")  // Status
  pnl             Float?    // Profit/Loss
  exitReason      String?   // Exit reason
  chat            Chat      @relation(...)
  createdAt       DateTime  @default(now())
  updatedAt       DateTime  @updatedAt
}
```

### Metrics Table (Performance Metrics)
```prisma
model Metrics {
  id        String   @id @default(cuid())
  name      String   // Metric name
  model     String   // Model version
  data      Json     // Metric data (JSON format)
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
}
```

### LessonLearned Table (Learning Feedback)
```prisma
model LessonLearned {
  id         String   @id @default(cuid())
  tradeId    String   // Associated trade ID
  symbol     String   // Trading pair
  outcome    String   // Result: profit/loss
  pnl        Float    // P&L amount
  lesson     String   @db.Text  // Lesson learned
  indicators Json     // Technical indicators snapshot
  createdAt  DateTime @default(now())
}
```

---

## 🤝 Contribution Guidelines

Welcome to submit Issues and Pull Requests!

Contact: email:2731468336@qq.com

---

## 📄 License

MIT License - See [LICENSE](LICENSE) file for details

---

## ⚠️ Disclaimer

**This project is for educational and research purposes only and does not constitute any investment advice. Cryptocurrency trading involves high risks and may result in partial or total loss of capital. All risks associated with using this system for live trading are borne by the user. The developers are not responsible for any trading losses.**

**Risk Warning:**
- 📉 Cryptocurrency markets are extremely volatile and can cause significant losses in short periods
- 🤖 AI systems cannot guarantee profits, past performance does not indicate future results
- 💰 Only invest funds you can afford to lose
- 📚 Please fully understand the associated risks before investing

---

**Version**: v1.0.0
**Last Updated**: November 10, 2025
**Maintenance Status**: 🟢 Actively Maintained