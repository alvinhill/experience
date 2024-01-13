![ATM](https://github.com/alvinhill/experience/assets/132315899/bc84c35b-c296-4af2-b648-18a6c328f8b0)


# ATM Program
## General Info
This program simulates an atm program.  It checks the pin code and gives you the option for withdrawal, deposits or see the statement.

This interface is linked to an SQL database.  It has two tables.  One is a customer table and the other is a transaction table.  The customer table has a primary key that links to each transaction made by each customer.

We can look at the statement.  This shows the related information is transaction order.  It also gives a running total and final balance.  
We can withdraw and/or look at other accounts.
It has an admin panel that can be used to do different queries.  
This program has three classes.  
It has an “action” class used to supply values for the selected tasks to perform.
It has a “main” class to provide the main interface and give numeric values and sound to the buttons.
It has a “result” class that is under construction.
It has a “state” statement class to show the account in the database.

It has a data1 class that 
1.)	Does the math for deposits and withdrawals.
2.)	 Connects to the data base.   
3.)	It stores the pin codes and the comparison method to control secure access.

It has a test class which is inactive now.
The upgrade path for this is:

See the video at my portfolio site:  http://alvinrainhill.com/EXP-X3.html

1.)	Upgrade the admin panel
2.)	Create other built-in queries to generate reports and totals for the admin panel.
3.)	Code a “Create New Account” for new customers.
4.)	Finish or delete the “results” and “test” classes.

# ATM CODE
## This class does several things.

1.)	It validates the pin code.
2.)	Supplies the transaction label.
3.)	Does the transaction math.
4.)	Opens the database and inputs the value into the database.

 class DATA1
    {
        private decimal balance ;

        private string pin;
        public decimal money;
        public string VCODE;
        public bool status= false ;
        // static public string INPUT { get; set; } = "7111";
        static public string INPUT;
        //= "7111";

        public string[] match = new string[10] { "9111", "7111", "8111", "4111", "5111", "6111", "3111", "2111", "1111", "1001"};// 10
      //public string[] match = new string[10] { "9111", "7111", "8111", "4111", "5111", "6111", "3111", "2111", "1111", "1001" };// 10

        public decimal BALANCE
        {
            get
            {
                return balance ;
            }
            set
            {
                balance  = value;
            }

        }

        public string PIN
        {
            get
            {
                return pin;
            }

            set
            {
                pin = value;

                for (int i = 0; i < match.Length ; i++)
                {
                    if (pin == match[i])
                    {
                        INPUT = pin;
                        status = true;
                      //  System.Windows.Forms.MessageBox.Show("GOOD");
                        
                        break;
                    }
                    else if (i ==9)//9
                    {
                        System.Windows.Forms.MessageBox.Show("BAD PIN");
                    }
                }
            }
        }
           public decimal MONEY
            {
            get
            {
                return money;
            }
            set
            {
                money = value;
            }
            }

        // DEPOSIT METHOD
        public decimal DEPOSIT()
        {
            balance = balance + money;
         if (money > 0)
           {
                VCODE = "DEPOSIT";
                RECORD();
         }
            return balance;
        }
        // WITHDRAWAL METHOD
        public decimal WITHDRAW()
        {
            balance = balance - money;
            if (balance < 0)
            {
                VCODE = "WITHDRAWAL";
                RECORD();
            }
            return balance;
        }
        public void RECORD()
        {
            // THIS WORKS TO PUT A VARIABLE INTO THE DATABASE !!!
           
            SqlConnection SQLCONNECT = new SqlConnection(@"Data Source = SATURN; Initial Catalog = NEWBANK; Integrated Security = true");
            SqlCommand SQLCMD = new SqlCommand("select * from ACCOUNTS2 WHERE PIN ='"+INPUT +"'", SQLCONNECT);

            SQLCONNECT.Open();
            SqlDataReader SQLREADER = SQLCMD.ExecuteReader();
            SQLREADER.Read();
            string DPIN;
            string DACCTNUMBER;
            DPIN = SQLREADER.GetValue(1).ToString();
            DACCTNUMBER = SQLREADER.GetValue(2).ToString();
            SQLCONNECT.Close();
            SQLCONNECT.Open();
            // ENTER DATA INTO DATABASE
            var NEWENTRY = "Insert into ACCOUNTS2(PIN,AcctNumber,TransData,CODE) values('" + DPIN + "','" + DACCTNUMBER + "'," + balance  + ", '" + VCODE + "')";// GOOD
            SQLCMD = new SqlCommand(Convert.ToString(NEWENTRY), SQLCONNECT);
            SQLCMD.ExecuteNonQuery();
            SQLCMD.Dispose();
            SQLCONNECT.Close();
        }
    }
