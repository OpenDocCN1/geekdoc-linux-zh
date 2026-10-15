
| 552 | ug=rx, o=w | r-x r-x --w |
| 554 | ug=rx, o=r | r-x r-x r-- |
| 555 | a=rx | r-x r-x r-x |
| 556 | ug=rx, o=rw | r-x r-x rw- |
| 557 | ug=rx, o=rwx | r-x r-x rwx |
| 560 | u=rx, g=rw | r-x rw- --- |
| 561 | u=rx, g=rw, o=x | r-x rw- --x |
| 562 | u=rx, g=rw, o=w | r-x rw- --w |
| 564 | u=rx, g=rw, o=r | r-x rw- r-- |
| 565 | uo=rx, g=rw | r-x rw- r-x |
| 566 | u=rx, go=rw | r-x rw- rw- |
| 567 | u=rx, g=rw, o=rwx | r-x rw- rwx |
| 570 | u=rx, g=rwx | r-x rwx --- |
| 571 | u=rx, g=rwx, o=x | r-x rwx --x |
| 572 | u=rx, g=rwx, o=w | r-x rwx --w |
| 574 | u=rx, g=rwx, o=r | r-x rwx r-- |
| 575 | uo=rx, g=rwx | r-x rwx r-x |
| 576 | u=rx, g=rwx, o=rw | r-x rwx rw- |
| 577 | u=rx, go=rwx | r-x rwx rwx |
| 600 | u=rw | rw- --- --- |
| 601 | u=rw, o=x | rw- --- --x |
| 602 | u=rw, o=w | rw- --- --w |
| 604 | u=rw, o=r | rw- --- r-- |
| 605 | uo=rw | rw- --- r-x |
| 606 | u=rw, go=r | rw- --- rw- |
| 607 | u=rw, o=rwx | rw- --- rwx |
| 610 | u=rw, g=x | rw- --- --x |
| 611 | u=rw, go=x | rw- --x --x |
| 612 | u=rw, g=x, o=w | rw- --x --w |
| 614 | u=rw, g=x, o=r | rw- --x r-- |
| 615 | u=rw, o=r, g=x | rw- --x r-x |
| 616 | uo=rw, g=x | rw- --x rw- |
| 617 | u=rw, g=x, o=rwx | rw- --x rwx |
| 620 | u=rw, g=w | rw- --w --- |
| 621 | u=rw, g=w, o=x | rw- --w --x |
| 622 | u=rw, go=w | rw- --w --w |
| 624 | u=rw, g=w, o=r | rw- --w r-- |
| 625 | u=rw, g=w, o=rx | rw- --w r-x |
| 626 | uo=rw, g=w | rw- --w rw- |
| 627 | u=rw, g=w, o=rwx | rw- --w rwx |
| 640 | u=rw, g=r | rw- r-- --- |
| 641 | u=rw, g=r, o=x | rw- r-- --x |
| 642 | u=rw, g=r, o=w | rw- r-- --w |
| 644 | u=rw, go=r | rw- r-- r-- |
| 645 | u=rw, g=r, o=rx | rw- r-- r-x |
| 646 | uo=rw, g=r | rw- r-- rw- |
| 647 | u=rw, g=r, o=rwx | rw- r-- rwx |
| 650 | u=rw, g=rx | rw- r-x --- |
| 651 | u=rw, g=rx, o=x | rw- r-x --x |
| 652 | u=rw, g=rx, o=w | rw- r-x --w |
| 654 | u=rw, g=rx, o=r | rw- r-x r-- |
| 655 | a=rx | rw- r-x r-x |
| 656 | ug=rx, o=rw | rw- r-x rw- |
| 657 | ug=rx, o=rwx | rw- r-x rwx |
| 660 | ug=rw | rw- rw- --- |
| 661 | u=rw, g=rw, o=x | rw- rw- --x |
| 662 | u=rw, g=rw, o=w | rw- rw- --w |
| 664 | ug=rw, o=r | rw- rw- r-- |
| 665 | ug=rw, o=rx | rw- rw- r-x |
| 666 | a=rw | rw- rw- rw- |
| 667 | ug=rw, o=rwx | rw- rw- rwx |
| 670 | u=rw, g=rwx | rw- rwx --- |
| 671 | u=rw, g=rwx, o=x | rw- rwx --x |
| 672 | u=rw, g=rwx, o=w | rw- rwx --w |
| 674 | u=rw, g=rwx, o=r | rw- rwx r-- |
| 675 | u=r, g=rw, o=r | r-x rwx r-- |
| 676 | uo=rw, g=rwx | r-x rwx rw- |
| 677 | u=rw, go=rwx | rwx rwx rwx |
| 700 | u=rwx | rwx --- --- |
| 701 | u=rwx, o=x | rwx --- --x |
| 702 | u=rwx, o=w | rwx --- --w |
| 704 | u=rwx, o=r | rwx --- r-- |
| 705 | uo=r | rwx --- r-x |
| 706 | u=rwx, o=rw | rwx --- rw- |
| 707 | uo=rwx | rwx --- rwx |
| 710 | u=rwx, g=x | rwx --x --- |
| 711 | u=rwx, go=x | rwx --x --x |
| 712 | u=rwx, g=x, o=w | rwx --x --w |
| 714 | u=rwx, g=x, o=r | rwx --x r-- |
| 715 | u=rwx, o=r, g=x | rwx --x r-x |
| 716 | u=rwx, o=r, g=x | rwx --x rw- |
| 717 | uo=rwx, g=x | rwx --x rwx |
| 720 | u=rwx, g=w | rwx --w --- |
| 721 | u=rwx, g=w, o=x | rwx --w --x |
| 722 | u=rwx, go=w | rwx --w --w |
| 724 | u=rwx, g=w, o=r | rwx --w r-- |
| 725 | u=rwx, g=w, o=r | rwx --w r-x |
| 726 | u=rwx, g=w, o=rw | rwx --w rw- |
| 727 | uo=rwx, g=w | rwx --w rwx |
| 740 | u=rwx, g=r | rwx r-- --- |
| 741 | u=rwx, g=r, o=x | rwx r-- --x |
| 742 | u=rwx, g=r, o=w | rwx r-- --w |
| 744 | u=rwx, g=r, o=r | rwx r-- r-- |
| 745 | u=rwx, g=r, o=rx | rwx r-- r-x |
| 746 | u=rwx, o=rw, g=r | rwx r-- rw- |
| 747 | u=rwx, go=r | rwx r-- rwx |
| 750 | u=rwx, g=rx | rwx r-x --- |
| 751 | u=rwx, g=rx, o=x | rwx r-x --x |
| 752 | u=rwx, g=rx, o=w | rwx r-x --w |
| 754 | u=rwx, g=r, o=- | rwx r-x --- |
| 755 | u=rwx, g=rx | rwx r-x r-x |
| 756 | u=rwx, g=rx, o=rw | rwx r-x rw- |
| 757 | u=rwx, g=rx, o=rwx | rwx r-x rwx |
| 760 | u=rwx, g=rw | rwx rw- ---
