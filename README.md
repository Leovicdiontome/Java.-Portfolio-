# Java.-Portfolio-
Project 

import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class InventoryGUI {
    private static final int ROWS = 4;
    private static final int COLUMNS = 5;
    private static final String EMPTY_SLOT = "Empty";
    
    private static int itemCount = 0;
    private static JLabel itemCountLabel;

    public static void main(String[] args) {
        JFrame frame = new JFrame("Inventory");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(700, 500);
        frame.setLayout(new BorderLayout());

        JPanel inventoryPanel = new JPanel(new GridLayout(ROWS, COLUMNS, 5, 5));
        JButton[][] inventorySlots = new JButton[ROWS][COLUMNS];

        itemCountLabel = new JLabel("Items in Inventory: 0");
        itemCountLabel.setHorizontalAlignment(SwingConstants.CENTER);
        itemCountLabel.setFont(new Font("Arial", Font.BOLD, 16));
        frame.add(itemCountLabel, BorderLayout.NORTH);

        for (int row = 0; row < ROWS; row++) {
            for (int col = 0; col < COLUMNS; col++) {
                JButton slot = new JButton(EMPTY_SLOT);
                slot.setBackground(Color.LIGHT_GRAY);
                slot.setFont(new Font("Arial", Font.PLAIN, 14));

                slot.addActionListener(e -> {
                    String[] options;
                    if (slot.getText().equals(EMPTY_SLOT)) {
                        options = new String[]{"Add Item", "Cancel"};
                    } else {
                        options = new String[]{"Remove Item", "Cancel"};
                    }

                    int choice = JOptionPane.showOptionDialog(
                        frame,
                        "Choose an action for this slot:",
                        "Slot Action",
                        JOptionPane.DEFAULT_OPTION,
                        JOptionPane.PLAIN_MESSAGE,
                        null,
                        options,
                        options[0]
                    );

                    if (slot.getText().equals(EMPTY_SLOT) && choice == 0) {
                        String itemName = JOptionPane.showInputDialog("Enter item name:");
                        if (itemName != null && !itemName.trim().isEmpty()) {
                            slot.setText(itemName.trim());
                            slot.setBackground(Color.GREEN);
                            itemCount++;
                            updateItemCount();
                        }
                    } else if (!slot.getText().equals(EMPTY_SLOT) && choice == 0) {
                        slot.setText(EMPTY_SLOT);
                        slot.setBackground(Color.LIGHT_GRAY);
                        itemCount--;
                        updateItemCount();
                    }
                });

                inventorySlots[row][col] = slot;
                inventoryPanel.add(slot);
            }
        }

        frame.add(inventoryPanel, BorderLayout.CENTER);
        frame.setVisible(true);
    }

    private static void updateItemCount() {
        itemCountLabel.setText("Items in Inventory: " + itemCount);
    }
}
