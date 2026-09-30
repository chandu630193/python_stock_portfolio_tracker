# python_stock_portfolio_tracker
def main():
    # 1. Hardcoded dictionary defining stock prices
    stock_prices = {
        "AAPL": 180.00,
        "TSLA": 250.00,
        "GOOGL": 140.00,
        "MSFT": 330.00,
        "AMZN": 135.00
    }

    portfolio = {}
    total_investment = 0.0

    print("Welcome to the Simple Stock Portfolio Tracker!")
    print(f"Available stocks to track: {', '.join(stock_prices.keys())}")

    # 2. User Input Loop
    while True:
        tracker = input("\nEnter the stock tracker (or type 'done' to finish): ").upper()
        
        if tracker == 'DONE':
            break
            
        if tracker not in stock_prices:
            continue
            
        try:
            quantity = float(input(f"Enter the number of shares you own for {tracker}: "))
        except ValueError:
            print("Invalid input. Please enter a valid number.")
            continue

        # Update portfolio dictionary
        portfolio[tracker] = portfolio.get(tracker, 0) + quantity
        print(f"Added {quantity} shares of {tracker} to your portfolio.")

    # 3. Basic Arithmetic & Display
    print("\n" + "="*30)
    print("PORTFOLIO SUMMARY")
    print("="*30)
    
    summary_lines = []
    for tracker, qty in portfolio.items():
        price = stock_prices[tracker]
        value = qty * price
        total_investment += value
        
        line = f"{tracker}: {qty} shares @ ${price:.2f} = ${value:.2f}"
        summary_lines.append(line)
        print(line)
        
    total_line = f"\nTOTAL INVESTMENT VALUE: ${total_investment:.2f}"
    summary_lines.append(total_line)
    print(total_line)
    print("="*30)

    # 4. Optional File Handling
    if total_investment > 0:
        save_choice = input("\nWould you like to save this summary to a file? (y/n): ").lower()
        if save_choice == 'y':
            filename = "portfolio_summary.txt"
            with open(filename, "w") as file:
                file.write("PORTFOLIO SUMMARY\n")
                file.write("=================\n")
                for line in summary_lines:
                    file.write(line + "\n")
            print(f"Success! Your portfolio has been saved to {filename}")

if __name__ == "__main__":
    main()
