## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/hardlydifficult/Platformer/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

[Test](/Test.md)


<div style="font-size:5em">This is a test</div>
<details><summary>Hi</summary>You rock!

[Test](/Test.md)

```csharp
void Update_Animation(
    bool shouldFreeze = false)
  {
    if(animator.isActiveAndEnabled == false)
    {
      return;
    }

    animator.SetFloat("Speed", shouldFreeze ? 0 : player.myBody.velocity.magnitude);
    animator.SetBool("isGrounded", shouldFreeze ? false : player.feet.isGrounded);
    animator.SetBool("isClimbing", shouldFreeze ? false : player.ladderMovement.isOnLadder);
    animator.SetBool("hasWeapon", shouldFreeze ? false : player.currentWeapon != null);
  }
```

<br>
nailed it.
</details>

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/hardlydifficult/Platformer/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
