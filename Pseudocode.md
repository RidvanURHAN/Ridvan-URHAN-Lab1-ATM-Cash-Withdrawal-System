Pseudocode:

START
    // Initialization of dummy account data
    Set correct_PIN to 1234
    Set account_balance to 5000
    Set daily_limit to 2000
    Set pin_attempts to 0
    Set access_granted to FALSE
    Set continue_transaction to TRUE

    // Phase 1: PIN Verification (Maximum 3 attempts)
    LOOP WHILE pin_attempts < 3 AND access_granted == FALSE
        PRINT "Please enter your 4-digit PIN:"
        READ entered_PIN
        
        IF entered_PIN == correct_PIN THEN
            Set access_granted to TRUE
            PRINT "PIN accepted. Access granted."
        ELSE
            Set pin_attempts to pin_attempts + 1
            PRINT "Incorrect PIN."
            
            IF pin_attempts == 3 THEN
                PRINT "Maximum attempts reached. Your card has been retained."
                Set continue_transaction to FALSE
            END IF
        END IF
    END LOOP

    // Phase 2: Transaction Process
    IF access_granted == TRUE THEN
        LOOP WHILE continue_transaction == TRUE
            PRINT "Enter the amount you wish to withdraw (Must be a multiple of 20 TL):"
            READ withdrawal_amount
            
            // Phase 3: Validations (Multiples of 20, Balance, and Daily Limit)
            IF withdrawal_amount MOD 20 != 0 THEN
                PRINT "Error: Amount must be in multiples of 20 TL."
            ELSE
                IF withdrawal_amount > account_balance THEN
                    PRINT "Error: Insufficient funds. Your current balance is: " + account_balance + " TL."
                ELSE
                    IF withdrawal_amount > daily_limit THEN
                        PRINT "Error: Amount exceeds your remaining daily limit of: " + daily_limit + " TL."
                    ELSE
                        // Phase 4: Successful Transaction
                        Set account_balance to account_balance - withdrawal_amount
                        Set daily_limit to daily_limit - withdrawal_amount
                        
                        PRINT "Please take your cash: " + withdrawal_amount + " TL."
                        PRINT "Your new account balance is: " + account_balance + " TL."
                    END IF
                END IF
            END IF
            
            // Phase 5: Option to repeat the transaction
            PRINT "Would you like to perform another transaction? (Type YES or NO)"
            READ user_choice
            
            IF user_choice == "NO" THEN
                Set continue_transaction to FALSE
            END IF
            
        END LOOP
    END IF

    // End of session
    PRINT "Thank you for using our ATM. Please take your card."
END
