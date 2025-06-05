import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

class FrameExample extends JFrame implements ActionListener {
    JTextField ageField, output;
    JButton checkButton, resetButton;

    public FrameExample() {
        setTitle("Voting Eligibility Checker");
        setSize(300, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocation(500, 300);

        JPanel panel = new JPanel();
        panel.setLayout(null);
        add(panel);

        JLabel ageLabel = new JLabel("Enter Age:");
        ageLabel.setBounds(30, 30, 100, 20);
        panel.add(ageLabel);

        ageField = new JTextField();
        ageField.setBounds(100, 30, 100, 20);
        panel.add(ageField);

        checkButton = new JButton("Check");
        resetButton = new JButton("Reset");
        checkButton.setBounds(50, 80, 100, 30);
        resetButton.setBounds(160, 80, 80, 30);
        panel.add(checkButton);
        panel.add(resetButton);

        checkButton.addActionListener(this);
        resetButton.addActionListener(this);

        output = new JTextField();
        output.setBounds(50, 140, 190, 25);
        output.setEditable(false);  // Prevent user typing into output
        panel.add(output);

        setVisible(true);
    }

    public void actionPerformed(ActionEvent ae) {
        if (ae.getSource() == checkButton) {
            try {
                int age = Integer.parseInt(ageField.getText());
                if (age >= 18) {
                    output.setText("Eligible to vote.");
                } else {
                    output.setText("Not eligible to vote.");
                }
            } catch (NumberFormatException e) {
                output.setText("Enter a valid numeric age.");
            }
        } else if (ae.getSource() == resetButton) {
            ageField.setText("");
            output.setText("");
        }
    }
}

public class GUIpractice {
    public static void main(String[] args) {
        new FrameExample();
    }
}


import java.io.*;
import java.util.Scanner;

public class ReverseWordInFile {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String filename = "reverse.txt";

        System.out.print("Enter a sentence: ");
        String inputSentence = scanner.nextLine();

        try (FileWriter writer = new FileWriter(filename)) {
            writer.write(inputSentence);
        } catch (IOException e) {
            System.out.println("Error writing to file: " + e.getMessage());
            return;
        }

        String readSentence = "";
        try (BufferedReader reader = new BufferedReader(new FileReader(filename))) {
            readSentence = reader.readLine();
        } catch (IOException e) {
            System.out.println("Error reading from file: " + e.getMessage());
            return;
        }

        String[] words = readSentence.split(" ");

        System.out.println("Sentence with each word reversed:");
        for (String word : words) {
            StringBuffer reversedWord = new StringBuffer(word);
            System.out.print(reversedWord.reverse() + " ");
        }
    }
}
