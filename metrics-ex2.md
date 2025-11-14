Cyclomatic complexity of method "loadFromText"

public int loadFromText(String text): 8
Lines of decision point : 162, 163, 188, 190, 191, 192, 195, 199

The "finally" part can be done in helper methods that closes a Scanner and a FileInputStream object to avoid nesting
try-catch everywhere we need to manage this.
We could name them closeFISObject and closeScannerObject.

The CC went down to 2 :
~ public int loadFromText(String text): 2