Cropping away negative impacts of line height 
based on https://medium.com/eightshapes-llc/cropping-away-negative-impacts-of-line-height-84d744e016ce

```
import styled from "styled-components";
import { textCrop } from "../path-to-textCrop"

export const Label = styled.span`
  color: #D83C4C;
  ${textCrop};
`
```

```
import { css } from "styled-components";

export const textCrop = (() => {
  const lineHeight = 1.3;
  const topAdjustment = 0;
  const bottomAdjustment = 0;
  const topCrop = 4;
  const bottomCrop = 11;
  const cropFontSize = 32;
  const cropLineHeight = 1.2;

  const dynamicTopCrop =
    (topCrop + (lineHeight - cropLineHeight) * (cropFontSize / 2)) /
    cropFontSize;

  const dynamicBottomCrop =
    (bottomCrop + (lineHeight - cropLineHeight) * (cropFontSize / 2)) /
    cropFontSize;

  const marginBottom = `-${dynamicTopCrop + topAdjustment}em`;

  const marginTop = `-${dynamicBottomCrop + bottomAdjustment}em`;

  return css`
    line-height: ${lineHeight};

    &::before,
    &::after {
      content: "";
      display: block;
      height: 0;
      width: 0;
    }
    &::before {
      margin-bottom: ${marginBottom};
    }
    &::after {
      margin-top: ${marginTop};
    }
  `;
})()
```
