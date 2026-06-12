import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.HashMap;
import java.util.Map;
import java.util.Random;

public class OnlineReservationSystem extends JFrame {

    // Centralized In-Memory Database to store reservations (PNR -> Ticket Details)
    private static final Map<String, Ticket> database = new HashMap<>();
    
    // Mock Train Data (Train Number -> Train Name)
    private static final Map<String, String> trainMap = new HashMap<>();
    static {
        trainMap.put("12345", "Express Bullet");
        trainMap.put("67890", "Metropolitan Trans");
        trainMap.put("11223", "Coastal Cruiser");
        trainMap.put("44556", "Grand Orient");
    }

    // CardLayout to switch between different modules/forms
    private CardLayout cardLayout;
    private JPanel mainPanel;

    public OnlineReservationSystem() {
        setTitle("Online Reservation System");
        setSize(500, 450);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        cardLayout = new CardLayout();
        mainPanel = new JPanel(cardLayout);

        // Adding Modules to the main panel
        mainPanel.add(createLoginPanel(), "Login");
        mainPanel.add(createMainMenuPanel(), "MainMenu");
        mainPanel.add(createReservationPanel(), "Reservation");
        mainPanel.add(createCancellationPanel(), "Cancellation");

        add(mainPanel);
        cardLayout.show(mainPanel, "Login");
    }

    // --- 1. LOGIN MODULE ---
    private JPanel createLoginPanel() {
        JPanel panel = new JPanel(new GridBagLayout());
        panel.setBorder(BorderFactory.createTitledBorder("Login Form"));
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(10, 10, 10, 10);
        gbc.fill = GridBagConstraints.HORIZONTAL;

        JLabel userLabel = new JLabel("Username:");
        JTextField userField = new JTextField(15);
        JLabel passLabel = new JLabel("Password:");
        JPasswordField passField = new JPasswordField(15);
        JButton loginButton = new JButton("Login");

        // Simple hardcoded authorized credentials
        userField.setText("admin");
        passField.setText("password");

        gbc.gridx = 0; gbc.gridy = 0; panel.add(userLabel, gbc);
        gbc.gridx = 1; panel.add(userField, gbc);
        gbc.gridx = 0; gbc.gridy = 1; panel.add(passLabel, gbc);
        gbc.gridx = 1; panel.add(passField, gbc);
        gbc.gridx = 0; gbc.gridy = 2; gbc.gridwidth = 2;
        panel.add(loginButton, gbc);

        loginButton.addActionListener(e -> {
            String username = userField.getText();
            String password = new String(passField.getPassword());

            if (username.equals("admin") && password.equals("password")) {
                JOptionPane.showMessageDialog(panel, "Login Successful!");
                cardLayout.show(mainPanel, "MainMenu");
            } else {
                JOptionPane.showMessageDialog(panel, "Invalid ID or Password.", "Error", JOptionPane.ERROR_MESSAGE);
            }
        });

        return panel;
    }

    // --- MAIN MENU DASHBOARD ---
    private JPanel createMainMenuPanel() {
        JPanel panel = new JPanel(new GridLayout(3, 1, 10, 10));
        panel.setBorder(BorderFactory.createEmptyBorder(50, 50, 50, 50));

        JButton resButton = new JButton("Go to Reservation Form");
        JButton cancelButton = new JButton("Go to Cancellation Form");
        JButton logoutButton = new JButton("Logout");

        panel.add(resButton);
        panel.add(cancelButton);
        panel.add(logoutButton);

        resButton.addActionListener(e -> cardLayout.show(mainPanel, "Reservation"));
        cancelButton.addActionListener(e -> cardLayout.show(mainPanel, "Cancellation"));
        logoutButton.addActionListener(e -> cardLayout.show(mainPanel, "Login"));

        return panel;
    }

    // --- 2. RESERVATION MODULE ---
    private JPanel createReservationPanel() {
        JPanel panel = new JPanel(new GridBagLayout());
        panel.setBorder(BorderFactory.createTitledBorder("Reservation Form"));
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(5, 5, 5, 5);
        gbc.fill = GridBagConstraints.HORIZONTAL;

        JTextField nameField = new JTextField(15);
        JTextField ageField = new JTextField(5);
        JComboBox<String> trainNoCombo = new JComboBox<>(trainMap.keySet().toArray(new String[0]));
        JTextField trainNameField = new JTextField(15);
        trainNameField.setEditable(false);
        // Set initial auto-fill train name
        trainNameField.setText(trainMap.get(trainNoCombo.getSelectedItem()));

        JComboBox<String> classCombo = new JComboBox<>(new String[]{"AC First Class", "AC 2 Tier", "Sleeper", "General"});
        JTextField dateField = new JTextField("2026-12-25", 10);
        JTextField fromField = new JTextField(10);
        JTextField toField = new JTextField(10);

        JButton insertButton = new JButton("Insert");
        JButton backButton = new JButton("Back to Menu");

        // Auto-fill train name logic when train number changes
        trainNoCombo.addActionListener(e -> {
            String selectedNo = (String) trainNoCombo.getSelectedItem();
            trainNameField.setText(trainMap.get(selectedNo));
        });

        // Layout Components
        int row = 0;
        gbc.gridx = 0; gbc.gridy = row; panel.add(new JLabel("Passenger Name:"), gbc);
        gbc.gridx = 1; panel.add(nameField, gbc);

        row++;
        gbc.gridx = 0; gbc.gridy = row; panel.add(new JLabel("Age:"), gbc);
        gbc.gridx = 1; panel.add(ageField, gbc);

        row++;
        gbc.gridx = 0; gbc.gridy = row; panel.add(new JLabel("Train No:"), gbc);
        gbc.gridx = 1; panel.add(trainNoCombo, gbc);

        row++;
        gbc.gridx = 0; gbc.gridy = row; panel.add(new JLabel("Train Name:"), gbc);
        gbc.gridx = 1; panel.add(trainNameField, gbc);

        row++;
        gbc.gridx = 0; gbc.gridy = row; panel.add(new JLabel("Class Type:"), gbc);
        gbc.gridx = 1; panel.add(classCombo, gbc);

        row++;
        gbc.gridx = 0; gbc.gridy = row; panel.add(new JLabel("Date of Journey:"), gbc);
        gbc.gridx = 1; panel.add(dateField, gbc);

        row++;
        gbc.gridx = 0; gbc.gridy = row; panel.add(new JLabel("From:"), gbc);
        gbc.gridx = 1; panel.add(fromField, gbc);

        row++;
        gbc.gridx = 0; gbc.gridy = row; panel.add(new JLabel("To Destination:"), gbc);
        gbc.gridx = 1; panel.add(toField, gbc);

        row++;
        gbc.gridx = 0; gbc.gridy = row; panel.add(insertButton, gbc);
        gbc.gridx = 1; panel.add(backButton, gbc);

        // Action when 'Insert' button is pressed
        insertButton.addActionListener(e -> {
            if (nameField.getText().isEmpty() || fromField.getText().isEmpty() || toField.getText().isEmpty()) {
                JOptionPane.showMessageDialog(panel, "Please fill in all mandatory fields.", "Warning", JOptionPane.WARNING_MESSAGE);
                return;
            }

            // Generate a random unique 5-digit PNR
            String pnr = String.valueOf(10000 + new Random().nextInt(90000));
            
            Ticket ticket = new Ticket(
                    pnr,
                    nameField.getText(),
                    ageField.getText(),
                    (String) trainNoCombo.getSelectedItem(),
                    trainNameField.getText(),
                    (String) classCombo.getSelectedItem(),
                    dateField.getText(),
                    fromField.getText(),
                    toField.getText()
            );

            // Save to central database
            database.put(pnr, ticket);

            JOptionPane.showMessageDialog(panel, "Reservation Successful!\nYour generated PNR is: " + pnr, "Success", JOptionPane.INFORMATION_MESSAGE);
            
            // Clear inputs
            nameField.setText("");
            ageField.setText("");
            fromField.setText("");
            toField.setText("");
            cardLayout.show(mainPanel, "MainMenu");
        });

        backButton.addActionListener(e -> cardLayout.show(mainPanel, "MainMenu"));

        return panel;
    }

    // --- 3. CANCELLATION MODULE ---
    private JPanel createCancellationPanel() {
        JPanel panel = new JPanel(new BorderLayout(10, 10));
        panel.setBorder(BorderFactory.createTitledBorder("Cancellation Form"));

        JPanel topPanel = new JPanel(new FlowLayout());
        JLabel pnrLabel = new JLabel("Enter PNR Number:");
        JTextField pnrField = new JTextField(10);
        JButton fetchButton = new JButton("Submit PNR");
        topPanel.add(pnrLabel);
        topPanel.add(pnrField);
        topPanel.add(fetchButton);

        JTextArea infoArea = new JTextArea();
        infoArea.setEditable(false);
        infoArea.setBorder(BorderFactory.createLineBorder(Color.GRAY));
        infoArea.setText("\n   Submit a valid PNR number to fetch ticket details.");

        JPanel bottomPanel = new JPanel(new FlowLayout());
        JButton okButton = new JButton("OK (Confirm Cancel)");
        JButton backButton = new JButton("Back to Menu");
        okButton.setEnabled(false); // Only active if a ticket is found
        bottomPanel.add(okButton);
        bottomPanel.add(backButton);

        panel.add(topPanel, BorderLayout.NORTH);
        panel.add(new JScrollPane(infoArea), BorderLayout.CENTER);
        panel.add(bottomPanel, BorderLayout.SOUTH);

        // Final PNR variable tracker for closure confirmation
        final String[] targetPNR = new String[1];

        fetchButton.addActionListener(e -> {
            String enteredPnr = pnrField.getText().trim();
            if (database.containsKey(enteredPnr)) {
                Ticket ticket = database.get(enteredPnr);
                infoArea.setText(ticket.toString());
                targetPNR[0] = enteredPnr;
                okButton.setEnabled(true);
            } else {
                infoArea.setText("\n   No record found for PNR: " + enteredPnr);
                okButton.setEnabled(false);
                targetPNR[0] = null;
            }
        });

        // Action when 'OK' button is pressed to confirm cancellation
        okButton.addActionListener(e -> {
            if (targetPNR[0] != null) {
                database.remove(targetPNR[0]);
                JOptionPane.showMessageDialog(panel, "Ticket with PNR " + targetPNR[0] + " has been successfully canceled.", "Canceled", JOptionPane.INFORMATION_MESSAGE);
                infoArea.setText("\n   Ticket Canceled.");
                pnrField.setText("");
                okButton.setEnabled(false);
                targetPNR[0] = null;
            }
        });

        backButton.addActionListener(e -> {
            pnrField.setText("");
            infoArea.setText("\n   Submit a valid PNR number to fetch ticket details.");
            okButton.setEnabled(false);
            cardLayout.show(mainPanel, "MainMenu");
        });

        return panel;
    }

    // --- TICKET MODEL DATA CLASS ---
    private static class Ticket {
        String pnr, name, age, trainNo, trainName, classType, date, from, to;

        public Ticket(String pnr, String name, String age, String trainNo, String trainName, String classType, String date, String from, String to) {
            this.pnr = pnr;
            this.name = name;
            this.age = age;
            this.trainNo = trainNo;
            this.trainName = trainName;
            this.classType = classType;
            this.date = date;
            this.from = from;
            this.to = to;
        }

        @Override
        public String toString() {
            return String.format(
                    " --- TICKET DETAILS ---\n" +
                    " PNR Number      : %s\n" +
                    " Passenger Name  : %s (Age: %s)\n" +
                    " Train Details   : #%s - %s\n" +
                    " Class Type      : %s\n" +
                    " Date of Journey : %s\n" +
                    " Route           : From %s to %s\n" +
                    " -----------------------",
                    pnr, name, age, trainNo, trainName, classType, date, from, to
            );
        }
    }

    public static void main(String[] args) {
        // Run GUI codes on the Event Dispatch Thread for thread safety
        SwingUtilities.invokeLater(() -> new OnlineReservationSystem().setVisible(true));
    }
}
