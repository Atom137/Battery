
const int numberOfCells =2; // Number of cells in your battery pack

// Define the analog pins connected to each cell
const int cellPins[numberOfCells] = {A0,A1};

// Reference voltage for the ADC, typically 5V or 3.3V
const float referenceVoltage =5.0;

void setup() {
  Serial.begin(9600); // Initialize serial communication at 9600 baud rate
  for (int i = 0; i < numberOfCells; i++) {
    pinMode(cellPins[i], INPUT); // Set each pin as an input
  }
}

void loop() {
  float cell2= 0; // Variable to store the total voltage
  unsigned long currentTime = millis(); // Get the current elapsed time

  // Convert milliseconds to seconds
  float elapsedTime = currentTime / 1000.0;

  Serial.print("Elapsed Time: ");
  Serial.print(elapsedTime, 2); // Print elapsed time with 2 decimal places
  Serial.println(" s");

  Serial.println("Cell Voltages:");

  for (int i = 0; i < numberOfCells; i++) {
    int analogValue = analogRead(cellPins[i]); // Read the analog value
    float cellVoltage = (analogValue / 1023.0) * referenceVoltage; // Convert to voltage
    cell2=-(2*cellVoltage)-cell2;  
    
  }
    Serial.print("Total Voltage:");
    int analogValue = analogRead(cellPins[0]);
    float cellVoltage = (analogValue / 1023.0)*referenceVoltage;
    Serial.print(cellVoltage*2,4);
    Serial.println(" V");
    Serial.print("Cell 1:");
    analogValue = analogRead(cellPins[1]);
    cellVoltage =(analogValue / 1023.0)*referenceVoltage;
    Serial.print(cellVoltage*2,4);
    Serial.println(" V");
    Serial.print("Cell 2");
    Serial.print(": ");
    Serial.print(cell2, 4); // Print the voltage with 4 decimal places
    Serial.println(" V");
  delay(2000); // Wait for 1 second before reading again
}
