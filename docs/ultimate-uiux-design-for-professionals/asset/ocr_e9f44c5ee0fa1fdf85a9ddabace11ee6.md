```
implementation.
/* Mobile-first styles */
body {
  font-size: 14px;
}
.header {
  display: block;
}
.nav-menu {
  display: none;
}
/* Tablet and larger screens */
@media (min-width: 768px) {
  body {
    font-size: 16px;
  }
  .nav-menu {
    display: block;
  }
}
/* Desktop and larger screens */
@media (min-width: 1024px) {
  .header {
    display: flex;
  }
}
```

The foundation styles in this illustration are made for mobile devices. Additional styles are applied when the screen width grows in order to modify the functionality and layout for tablets and desktops. This methodology guarantees that the essential features are tailored for mobile users, all the while offering a better viewing experience on bigger displays.

# Linking Mobile-First with Responsive Design

Responsive Web Design (RWD) and Mobile-First Design are closely connected, as both focus on delivering a good user experience across different devices and screen sizes. However, they use distinct strategies to achieve this goal.

**Key Connections:**