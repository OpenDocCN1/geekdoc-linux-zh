
```
        centerY = centerY + 4

        centerY2 = centerY2 + 2

    end

end

if pY - 2 > gheight / 2 then

    if centerY > ( gheight / 2 ) - ( gheight / 20 ) then

        centerY = centerY - 4

        centerY2 = centerY2 - 2

    end

end

colour = yellow

c = cos( pAngle + 90 ) // correct the view angle by 90 degrees

s = sin( pAngle + 90 )

u = gheight / 80 // scale the player ship to the resolution
```

### rotate & scale coordinates; draw player ship

```
polystart

polypot((u*(5 * c) - (u*5 * s) + pX), (u*(5 * s) + (u*(5 * c) + pY))

polypot((u*(5 * c) + pX), (u*(5 * s) + pY))

polypot((0 - (u*2 * s) + pX), (u*(-2 * s) + pY))

polypot((u*(-4 * c) + pX), (u*(-5 * s) + pY))

polypot((u*(-5 * c) - (u*(5 * s) + pX), (u*(-5 * s) + (u*(5 * c) + pY))

polypot((0 - (u*4 * s) + pX), (u*(-4 * s) + pY))

polypot((u*(-7 * c) + pX), (u*(-7 * s) + pY))

polypot((u*(7 * c) + pX), (u*(7 * s) + pY))

polyend

update

repeat

end
```
