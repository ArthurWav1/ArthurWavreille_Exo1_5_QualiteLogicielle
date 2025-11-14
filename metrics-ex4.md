Issue 1 :

Remove this unused method parameter "accManager". Bank.java:141

The method saveAccounts from the Bank class has a parameter that is never used inside of the method, it is useless but more importantly, it means that it asks for an object that is not necessary to its use which can make the method unusable.


Issue 2 : 

Remove this expression which always evaluates to "true" [+2 locations]. Person.java:150

The method which this sonarqube rule is refering to is validateGender, which returns true if gender is "M", "F", "m" or "f", else it throws an Exception.
The method setGender(the one where is located the sonarqube rule), should have a way of catching the exception and not just an if condition.

Issue 3 : 

A "NullPointerException" could be thrown; "fileScanner" is nullable here. [+2 locations]. BankAccount.java:163

In the method loadFromText, fileScanner is initialized with a null value, which means the while condition "while (fileScanner.hasNextLine())" will always throw a NullPointerException. This exception is only catch with the general "Exception" catch and it may take longer than necessary to notice that fileScanner is null, correcting the null value + added a more specific catch clause should be done to avoid wasting time on simple errors like this one.



Cleaning : 

Issue 1 is easily removed by just removing the parameter from the method definition and from its uses.
For Issue 3, I added a catch clause for the NullPointerException and I initialize the fileScanner (and the fis) by creating Scanner and FileInputStream objects BEFORE the while loop with a try-with-ressources logic.

NEW LOAD_FROM_TEXT METHOD :

public int loadFromText(String text) {
		int accountsLoaded = 0;
		Bank accManager = new Bank();

		try (FileInputStream fis = new FileInputStream(text);
			Scanner fileScanner = new Scanner(fis);) {
				while (fileScanner.hasNextLine()) { // 2

					BankAccount tmpAccount = new BankAccount();
					tmpAccount.setAccountNumber(fileScanner.nextInt());
					tmpAccount.setBalance(fileScanner.nextDouble());
					tmpAccount.setWithdrawLimit(fileScanner.nextDouble());
					tmpAccount.setDateCreated(fileScanner.next());
					String newName = fileScanner.next();
					char gender = fileScanner.next().charAt(0);
					int newAge = fileScanner.nextInt();
					float newWeight = fileScanner.nextFloat();
					float newHeight = fileScanner.nextFloat();
					String newHairColor = fileScanner.next();
					String newEyeColor = fileScanner.next();
					String newEmail = fileScanner.next();
					String accountHolder1 = newName + Person.DELIM + gender + Person.DELIM + newAge + Person.DELIM
							+ newHeight + Person.DELIM + newWeight + Person.DELIM + newHairColor + Person.DELIM
							+ newEyeColor + Person.DELIM + newEmail;
					Person accountHolderManager = new Person(accountHolder1);
					tmpAccount.setAccountHolder(accountHolderManager);
					accountsLoaded = accManager.addAccount(tmpAccount, 1);
				}
		} catch (FileNotFoundException e) {
			System.out.println("error while opening the file");
		} catch (NullPointerException e) {
			System.out.println("error while reading the file");
		} catch (Exception e){
			e.printStackTrace();
		}
		return accountsLoaded;
	}



In my opinion, it seems that sonarqube issues appears everywhere regardless of the WMC / CBO, the Bank file has much lower values but as much errors as the others.
