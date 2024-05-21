import javax.swing.*;
import java.awt.Color;
import java.awt.Image;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.table.DefaultTableModel;
import javax.tools.Tool;

public class firefliesGUI extends JFrame implements ActionListener {
    // Creating Buttons
    private JButton checkInBtn, checkOutBtn, regBtn, InfectedBtn, quitGameBtn;
    // JTable and Table Model
    private JTable infoTable;
    private DefaultTableModel tableModel;

    public firefliesGUI() {
        setTitle("Fireflies Data Base");
        setSize(500, 500);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLayout(null);

        // Set the Icon for application (Globally)
        setIconImage(new ImageIcon(getClass().getResource("/images/fireflies.png")).getImage());

        // Set Bounds GUI to screen center
        setLocationRelativeTo(null);

        checkInBtn = new JButton("Check In");
        checkInBtn.setBounds(50, 30, 120, 30);
        checkInBtn.addActionListener(this);
        // Custom Font & Background
        checkInBtn.setForeground(Color.WHITE);
        checkInBtn.setBackground(Color.BLACK);
        add(checkInBtn);
        //Custom Cursor 
        Image cursorImageCI = new ImageIcon(getClass().getResource("/images/checkincur.png")).getImage();
        Cursor customCursorCI = Toolkit.getDefaultToolkit().createCustomCursor(cursorImageCI, new Point(0,0), "cursorImageCI");
        checkInBtn.setCursor(customCursorCI);

        checkOutBtn = new JButton("Check Out");
        checkOutBtn.setBounds(50, 80, 120, 30);
        checkOutBtn.addActionListener(this);
        // Custom Font & Background
        checkOutBtn.setForeground(Color.WHITE);
        checkOutBtn.setBackground(Color.BLACK);
        add(checkOutBtn);
        //Custom Cursor
        Image cursorImageCO = new ImageIcon(getClass().getResource("/images/EllieC.png")).getImage();
        Cursor customCursorCO = Toolkit.getDefaultToolkit().createCustomCursor(cursorImageCO, new Point(0,0), "cursorImageCO");
        checkOutBtn.setCursor(customCursorCO);

        regBtn = new JButton("Sign In");
        regBtn.setBounds(50, 130, 120, 30);
        regBtn.addActionListener(this);
        // Custom Font & Background
        regBtn.setForeground(Color.WHITE);
        regBtn.setBackground(Color.BLACK);
        add(regBtn);

        InfectedBtn = new JButton("Infected Stages");
        InfectedBtn.setBounds(200, 30, 120, 30);
        InfectedBtn.addActionListener(this);
        // Custom Font & Background
        InfectedBtn.setForeground(Color.WHITE);
        InfectedBtn.setBackground(Color.RED);
        add(InfectedBtn);

        //Custom Cursor 
        Image cursorImageInfected = new ImageIcon(getClass().getResource("/images/Ellie.png")).getImage();
        Cursor customCursorInf = Toolkit.getDefaultToolkit().createCustomCursor(cursorImageInfected, new Point(0,0),"cursorImageInfected");
        InfectedBtn.setCursor(customCursorInf);

        // Initialize table model with column names
        tableModel = new DefaultTableModel(new Object[]{"Name", "Age", "Zone", "Favorite Weapon"}, 0);
        infoTable = new JTable(tableModel);

        // Add table to scroll pane
        JScrollPane scrollPane = new JScrollPane(infoTable);
        scrollPane.setBounds(50, 180, 400, 200);
        add(scrollPane);

        quitGameBtn = new JButton("Quit Game");
        quitGameBtn.setBounds(200, 400, 100, 30);
        quitGameBtn.addActionListener(this);
        // Custom Font & Background
        quitGameBtn.setForeground(Color.WHITE);
        quitGameBtn.setBackground(Color.BLACK);
        add(quitGameBtn);

        //Custom Cursor 
        Image cursorImageClear = new ImageIcon(getClass().getResource("/images/fireflies.png")).getImage();
        Cursor customCursorQuir = Toolkit.getDefaultToolkit().createCustomCursor(cursorImageClear, new Point(0,0), "customCursorQuir");
        quitGameBtn.setCursor(customCursorQuir);

        quitGameBtn.addActionListener(evt -> System.exit(0));

        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        if (e.getSource() == checkInBtn) {
            String name = JOptionPane.showInputDialog(null, "Type your name: ");
            String ageInput = JOptionPane.showInputDialog(null, "Enter your age: ");
            int age = Integer.parseInt(ageInput);
            String zone = JOptionPane.showInputDialog(null, "Enter your Zone: ");

            Object[] weapons = {"Semi-Auto Pistol", "Bolt-Action Rifle", "Revolver", "Pump Shotgun", "Bow", "Military Pistol", "Semi-Auto Rifle", "Hunting Pistol", "Double Barrel Shotgun", "Crossbow", "Flamethrower", "Silenced Submachine Gun"};
            int weaponChoice = JOptionPane.showOptionDialog(null, "Choose your favorite weapon:", "Favourite Weapon", JOptionPane.DEFAULT_OPTION, JOptionPane.QUESTION_MESSAGE, null, weapons, weapons[0]);

            if (weaponChoice != JOptionPane.CLOSED_OPTION) {
                String selectedWeapon = (String) weapons[weaponChoice];
                tableModel.addRow(new Object[]{name, age, zone, selectedWeapon});
            }
        } else if (e.getSource() == checkOutBtn) {
            int choice1 = JOptionPane.showOptionDialog(null, "Do you have any weapons with you?", "Check Out", JOptionPane.DEFAULT_OPTION, JOptionPane.QUESTION_MESSAGE, null, new String[]{"Yes", "No"}, "Yes");
            int choice2 = JOptionPane.showOptionDialog(null, "Will someone go with you?", "Check Out", JOptionPane.DEFAULT_OPTION, JOptionPane.QUESTION_MESSAGE, null, new String[]{"Yes", "No"}, "Yes");

            String weaponsMessage = "Weapons: " + (choice1 == 0 ? "Yes" : "No");
            String someoneGoingMessage = "Someone going with you: " + (choice2 == 0 ? "Yes" : "No");

            JOptionPane.showMessageDialog(this, weaponsMessage + "\n" + someoneGoingMessage, "Check Out Info", JOptionPane.INFORMATION_MESSAGE);
        } else if (e.getSource() == regBtn) {
            JOptionPane.showMessageDialog(this, "May Your Death Be Swift");
            tableModel.setRowCount(0);
        } else if (e.getSource() == InfectedBtn) {
            String defaultImagePath = "/images/SOI.jpg";
            ImageIcon defaultImageIcon = new ImageIcon(getClass().getResource(defaultImagePath));
            Image defaultImage = defaultImageIcon.getImage().getScaledInstance(200, 200, Image.SCALE_SMOOTH);
            JLabel defaultImageLabel = new JLabel(new ImageIcon(defaultImage));

            String[] options = {"Runner", "Stalker", "Clicker", "Shambler", "Bloater", "Rat king"};
            String[] imagePaths = {
                    "Runner.png",
                    "Stalker.png",
                    "Clicker.png",
                    "Shambler.png",
                    "Bloater.png",
                    "Ratking.png",
            };

            int choice = JOptionPane.showOptionDialog(this, defaultImageLabel, "Choose Infected Type", JOptionPane.DEFAULT_OPTION, JOptionPane.PLAIN_MESSAGE, null, options, options[0]);

            if (choice != JOptionPane.CLOSED_OPTION) {
                String selectedImagePath = "/images/infected/" + imagePaths[choice];
                ImageIcon selectedImageIcon = new ImageIcon(getClass().getResource(selectedImagePath));
                Image selectedImage = selectedImageIcon.getImage().getScaledInstance(100, 100, Image.SCALE_SMOOTH);
                JLabel selectedImageLabel = new JLabel(new ImageIcon(selectedImage));
                JOptionPane.showMessageDialog(this, selectedImageLabel, options[choice], JOptionPane.PLAIN_MESSAGE);
            }
        }
    }

    public static void main(String[] args) {
        new firefliesGUI();
    }
}
