---
title: "Smart Notes"
layout: post
categories: media
---

Smart Notes is a Java desktop app to have frequently copied text at hand, easy to copy. It sorts the texts sorted from most to least used, as seen in the picture above.
Link to Github repostory: [Smart Notes Github][smartnotes-github]

![Smart Notes app](/assets/smart_notes.png)


Below most of the code of the app. A scroll pane is added on top where the texts will be displayed. A copy button which copies a highlighted text to the clipboard is added next. Finally a field to add a new text is added, together with the button which adds the text to the scroll pane.

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

To create the GUI I have used Swing GUI Designer Intellij plugin.

[smartnotes-github]: https://github.com/viktorbobinski/SmartNotes
