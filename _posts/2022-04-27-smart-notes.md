---
title: "Smart Notes"
layout: post
categories: media
---

Smart Notes is a Java desktop app to manage notes. It allows to quickly copy notes and have most frequent used notes at hand. 

[Link to Github][smartnotes-github]

![Smart Notes app](/assets/smart_notes.png)


On top all notes are displayed. Once a note is highlighted, it can be copied with a button. 
The texts are sorted from most to least used, as seen in the picture above.
Below there is a field and button to insert new texts.

Below is most of the code of the app. 
A scroll pane is added on top where the texts will be displayed. 
A copy button which copies a highlighted text to the clipboard is added next. 
Finally a field to add a new text is added, together with the button which adds the text to the scroll pane.

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

The app is ready to be started:

{% highlight ruby %}
public class Main {

    public static void main(String[] args) {
        SmartNotes smartNotes = new SmartNotes();
        new GUI(smartNotes);
    }
}
{% endhighlight %}

All that is left is the SmartNotes class which is a container for the added texts.

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

To create the GUI I have used Swing GUI Designer Intellij plugin. This is why all Swing elements can be declared as global variables in the GUI class:

{% highlight ruby %}
private JButton copyButton;
private JButton addButton;
private JTextField textField;
private JLabel label;
private JScrollPane scrollPane;
private JPanel panel;
private JList list;
{% endhighlight %}

Their placement on the page gets set by the Swing GUI Designer plugin:

![Swing UI Designer in Intellij](/assets/smart_notes_ui_designer.png)

[smartnotes-github]: https://github.com/viktorbobinski/SmartNotes
