■Tavascript selectboxの中身をホバーで表示＆選択させたい。
-----------------------------------------------------------  
```tsx
'use client';

import React, { useRef } from 'react';

const HoverSelect: React.FC = () => {
  const selectRef = useRef<HTMLSelectElement>(null);

  const handleMouseEnter = () => {
    if (selectRef.current) {
      selectRef.current.size = selectRef.current.options.length;
    }
  };

  const handleMouseLeave = () => {
    if (selectRef.current) {
      selectRef.current.size = 1;
    }
  };

  const handleChange = () => {
    if (selectRef.current) {
      selectRef.current.size = 1;
    }
  };

  return (
    <div>
      <label htmlFor="language">言語を選択：</label>
      <select
        id="language"
        ref={selectRef}
        onMouseEnter={handleMouseEnter}
        onMouseLeave={handleMouseLeave}
        onChange={handleChange}
        size={1}
        style={{ width: '200px', fontSize: '16px' }}
      >
        <option value="ja">日本語</option>
        <option value="en">English</option>
        <option value="fr">Français</option>
        <option value="de">Deutsch</option>
      </select>
    </div>
  );
};

export default HoverSelect;
```
