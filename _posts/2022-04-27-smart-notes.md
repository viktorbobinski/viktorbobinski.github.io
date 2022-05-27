---
title: "SmartNotes"
layout: post
categories: media
---

SmartNotes is a Java desktop app to manage notes. It allows to quickly copy notes and have most frequent used notes at hand.

[SmartNotes on Github][smartnotes-github]

![SmartNotes app](/assets/smart_notes.png)


On top all notes are displayed. Once a note is highlighted, it can be copied with a button. <br />
The notes are sorted from most to least used, as seen in the picture above.


And below the code.

Every part of the UI is a `Swing` component. A scroll pane and button is added. Once the button is pressed the index from the `scrollPane` list is returned. This index is used to get the actual `String text` from the notes list.

{% highlight ruby %}
panel.add(scrollPane);
copyButton.setText("Copy!");
copyButton.addActionListener(e -> {
    int index = list.getSelectedIndex();
    if (index == -1) {
        return;
        }
    String selectedElement = smartNotes.getNote(index).toString().split(" / ")[0];
    StringSelection stringSelection = new StringSelection(selectedElement);
    Clipboard clipboard = Toolkit.getDefaultToolkit().getSystemClipboard();
    clipboard.setContents(stringSelection, null);
    list.setListData(smartNotes.notes.toArray());
});
panel.add(copyButton);
panel.add(textField);
addButton.setText("Add!");
addButton.addActionListener(e -> {
    String text = textField.getText();
    if (!text.equals("")) {
        smartNotes.addNote(text);
        list.setListData(smartNotes.notes.toArray());
    }
    textField.setText("");
});
panel.add(addButton);
{% endhighlight %}

After adding a few more lines to set the arrangement on the page...

{% highlight ruby %}
panel.setPreferredSize(new Dimension(1200, 400));
panel.setLayout(new GridLayout(5, 1));
label.setText("Smart Notes");
label.setHorizontalAlignment(0);
panel.add(label);
JFrame frame = new JFrame();
frame.add(panel, BorderLayout.CENTER);
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
frame.setTitle("Smart Notes");
frame.pack();
frame.setVisible(true);
{% endhighlight %}

...the app is ready to be started.

{% highlight ruby %}
public class Main {

    public static void main(String[] args) {
        SmartNotes smartNotes = new SmartNotes();
        new GUI(smartNotes);
    }
}
{% endhighlight %}

Finally, the `SmartNotes` class which is a container for the added texts. `SmartNotePair` is a pair of `String text` and `int usageCount`.

{% highlight ruby %}
public class SmartNotes {

    List<SmartNotePair> notes;

    public SmartNotes() {
        notes = new ArrayList<>();
    }

    public void addNote(String text) {
        SmartNotePair smartNotePair = new SmartNotePair();
        smartNotePair.setText(text);
        notes.add(smartNotePair);
    }

    public SmartNotePair getNote(int index) {
        String readNoteText = notes.get(index).getText();
        int readNoteUsageCount = notes.get(index).getUsageCount();

        for (int i = index - 1; i >= 0; --i) {
            int frontNoteUsageCount = notes.get(i).getUsageCount();
            if (frontNoteUsageCount < readNoteUsageCount) {
                String frontNoteText = notes.get(i).getText();
                notes.get(i).setText(readNoteText);
                notes.get(i).setUsageCount(readNoteUsageCount);
                notes.get(i + 1).setText(frontNoteText);
                notes.get(i + 1).setUsageCount(frontNoteUsageCount);
            }
        }

        return notes.get(index);
    }
}
{% endhighlight %}

The IntelliJ plugin `Swing GUI Designer` helps with the GUI creation. Thanks to this Swing elements can be declared as global variables in the GUI class...

{% highlight ruby %}
private JButton copyButton;
private JButton addButton;
private JTextField textField;
private JLabel label;
private JScrollPane scrollPane;
private JPanel panel;
private JList list;
{% endhighlight %}

... and their placement on the page gets set by the Swing GUI Designer plugin:

![Swing UI Designer in Intellij](/assets/smart_notes_ui_designer.png)

[smartnotes-github]: https://github.com/viktorbobinski/SmartNotes
