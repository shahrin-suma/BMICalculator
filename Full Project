package bmicalculator;

import javax.swing.*;
import java.awt.*;

public class BMICalculator extends JFrame {

    private JTextField weightField, heightField, feetField, inchField;
    private JLabel resultLabel;
    private JLabel tipLabel;
    private JProgressBar bmiBar;
    private JComboBox<String> unitBox;

    public BMICalculator() {

        setTitle("BMI Calculator");
        setSize(450, 430);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);
        setLayout(null);

        JLabel weightLabel = new JLabel("Enter Weight (kg):");
        weightLabel.setBounds(30, 30, 150, 25);
        add(weightLabel);

        weightField = new JTextField();
        weightField.setBounds(200, 30, 150, 25);
        add(weightField);

        JLabel unitLabel = new JLabel("Height Unit:");
        unitLabel.setBounds(30, 70, 150, 25);
        add(unitLabel);

        String[] units = {"Meters", "Centimeters", "Feet & Inches"};
        unitBox = new JComboBox<>(units);
        unitBox.setBounds(200, 70, 150, 25);
        add(unitBox);

        JLabel heightLabel = new JLabel("Enter Height:");
        heightLabel.setBounds(30, 110, 150, 25);
        add(heightLabel);

        heightField = new JTextField();
        heightField.setBounds(200, 110, 150, 25);
        add(heightField);

        feetField = new JTextField();
        feetField.setBounds(200, 110, 70, 25);
        add(feetField);

        inchField = new JTextField();
        inchField.setBounds(280, 110, 70, 25);
        add(inchField);

        JButton calcButton = new JButton("Calculate BMI");
        calcButton.setBounds(30, 160, 150, 35);
        calcButton.setBackground(new Color(46, 139, 87));
        calcButton.setForeground(Color.WHITE);
        add(calcButton);

        JButton resetButton = new JButton("Reset");
        resetButton.setBounds(200, 160, 150, 35);
        resetButton.setBackground(new Color(220, 20, 60));
        resetButton.setForeground(Color.WHITE);
        add(resetButton);

        resultLabel = new JLabel("Your BMI will appear here");
        resultLabel.setBounds(30, 210, 350, 30);
        add(resultLabel);

        tipLabel = new JLabel("An advice for you:");
        tipLabel.setBounds(30, 295, 350, 30);
        add(tipLabel);

        bmiBar = new JProgressBar(0, 100);
        bmiBar.setBounds(30, 255, 320, 30);
        bmiBar.setStringPainted(true);
        add(bmiBar);
        
        updateHeightFields();

        calcButton.addActionListener(e -> calculateBMI());
        resetButton.addActionListener(e -> resetFields());
        unitBox.addActionListener(e -> updateHeightFields());

        setVisible(true);
    }

    private void updateHeightFields() {
        String selected = unitBox.getSelectedItem().toString();
        if (selected.equals("Feet & Inches")) {
            heightField.setVisible(false);
            feetField.setVisible(true);
            inchField.setVisible(true);
        } else {
            heightField.setVisible(true);
            feetField.setVisible(false);
            inchField.setVisible(false);
        }
    }

    private void calculateBMI() {
        try {
            double weight = Double.parseDouble(weightField.getText());
            double heightInMeters = 0;

            if (weight <= 0) {
                showError("Weight must be positive.");
                return;
            }

            String unit = unitBox.getSelectedItem().toString();

            if (unit.equals("Meters")) {
                double h = Double.parseDouble(heightField.getText());
                if (h <= 0) 
                { 
                	showError("Height must be positive.");
                    return; 
                }
                heightInMeters = h;
            }
            else if (unit.equals("Centimeters")) {
                double h = Double.parseDouble(heightField.getText());
                if (h <= 0) 
                { 
                	showError("Height must be positive."); 
                	return; 
                }
                heightInMeters = h / 100.0;
            }
            else if (unit.equals("Feet & Inches")) {
                double feet = Double.parseDouble(feetField.getText());
                double inch = Double.parseDouble(inchField.getText());

                if (feet < 0 || inch < 0) 
                { 
                	showError("Height must be positive."); 
                	return; 
                }
                if (feet == 0 && inch == 0) 
                {
                    showError("Height must be greater than zero.");
                    return;
                }

                if (inch >= 12) 
                {
                    showError("Inches must be less than 12.");
                    return;
                }

                heightInMeters = (feet * 12 + inch) * 0.0254;
            }

            double bmi = weight / (heightInMeters * heightInMeters);
            String category;

            if (bmi < 18.5) {
                category = "Underweight";
                bmiBar.setValue(25);
                bmiBar.setForeground(Color.BLUE);
                tipLabel.setText("Try to eat more protein & calories.");
            } else if (bmi < 25) {
                category = "Normal weight";
                bmiBar.setValue(50);
                bmiBar.setForeground(Color.GREEN);
                tipLabel.setText("Great! Maintain a balanced diet.");
            } else if (bmi < 30) {
                category = "Overweight";
                bmiBar.setValue(75);
                bmiBar.setForeground(Color.ORANGE);
                tipLabel.setText("Try regular exercise & avoid junk food.");
            } else {
                category = "Obesity";
                bmiBar.setValue(100);
                bmiBar.setForeground(Color.RED);
                tipLabel.setText("Consult a doctor and start a weight-loss plan.");
            }

            resultLabel.setText(String.format("BMI: %.2f (%s)", bmi, category));
            bmiBar.setString(category);
            }
  
            catch (NumberFormatException ex) {
            showError("Please enter valid numbers.");
        }
    }

    private void resetFields() {
        weightField.setText("");
        heightField.setText("");
        feetField.setText("");
        inchField.setText("");

        resultLabel.setText("Your BMI will appear here");
        tipLabel.setText("An advice for you:");

        bmiBar.setValue(0);
        bmiBar.setString("");

        updateHeightFields();
    }

    private void showError(String msg) {
        resultLabel.setText(msg);
        bmiBar.setValue(0);
        bmiBar.setString("");
    }

    public static void main(String[] args) {
        new BMICalculator();
    }
}
