---
title: "Smart Notes"
layout: post
categories: media
---

![Smart Notes app](/assets/smart_notes.png)

Smart Notes is a Java desktop app to have frequently copied text at hand, easy to copy. It sorts the texts sorted from most to least used.

Example code snippet

{% highlight ruby %}
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

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
