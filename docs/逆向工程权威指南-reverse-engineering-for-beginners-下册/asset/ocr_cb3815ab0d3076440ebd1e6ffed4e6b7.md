```
ptr=0x007A49A8 M_left=0x007A4BA0 M_parent=0x007A4B80
M_right=0x007A4C40 M_color=0
key-20 value=[twenty]
ptr=0x007A4BA0 M_left=0x007A4C80 M_parent=0x007A49A8
M_right=0x00000000 M_color=1
key-12 value=[twelve]
ptr=0x007A4C80 M_left=0x00000000 M_parent=0x007A4B80
M_right=0x00000000 M_color=0
key-11 value=[eleven]
ptr=0x007A4C40 M_left=0x00000000 M_parent=0x007A49A8
M_right=0x00000000 M_color=1
key-99 value=[ninety-nine]
ptr=0x007A4B60 M_left=0x007A4B60 M_parent=0x007A4B80
M_right=0x007A4CA0 M_color=0
key-107 value=[one hundred seven]
ptr=0x007A4B60 M_left=0x00000000 M_parent=0x007A4BC0
M_right=0x00000000 M_color=1
key-101 value=[one hundred]
ptr=0x007A4CA0 M_left=0x00000000 M_parent=0x007A4BC0
M_right=0x007A4CC0 M_color=1
key-1001 value=[one thousand one]
ptr=0x007A4CC0 M_left=0x00000000 M_parent=0x007A4CA0
M_right=0x00000000 M_color=0
key-1010 value=[one thousand ten]
as a tree:
root----10 [ten]
L-----1 [one]
  L-----0 [zero]
  R-----5 [five]
    L-----3 [three]
      L-----2 [two]
      R-----6 [six]
    R-----9 [nine]
  R-----100 [one hundred]
    L-----20 [twenty]
      L-----12 [twelve]
        L-----11 [eleven]
        R-----99 [ninety-nine]
      R-----107 [one hundred seven]
        L-----101 [one hundred one]
          R-----1001 [one thousand one]
            R-----1010 [one thousand ten]
m.begin():
ptr=0x007A4BE0 M_left=0x00000000 M_parent=0x007A4C00
M_right=0x00000000 M_color=1
key-0 value=[zero]
m.end():
ptr=0x00028FE40 M_left=0x007A4BE0 M_parent=0x007A4988
```