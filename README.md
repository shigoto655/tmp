```tsx
'use client';

import React, { useState } from 'react';

const options = [
	{ value: 'ja', label: '日本語' },
	{ value: 'en', label: 'English' },
];

const AnimatedSelect: React.FC = () => {
	const [isOpen, setIsOpen] = useState(false);
	const [selected, setSelected] = useState(options[0]);

	const handleMouseEnter = () => setIsOpen(true);
	const handleMouseLeave = () => setIsOpen(false);
	const handleSelect = (option: (typeof options)[0]) => {
		setSelected(option);
		setIsOpen(false);
		handleButtonClick(option.value);
	};

	// ボタンを押したら「http://localhost:3000/ロケール/Top」のロケールを変更する関数
	const handleButtonClick = (locale: string) => {
		try {
			const url = `/${locale}/Top`;
			window.location.assign(url);
		} catch (error) {
			console.error('Navigation error:', error);
		}
	};

	return (
		<div style={{ display: 'flex', alignItems: 'flex-start', gap: '8px', position: 'relative' }}>
			<label htmlFor="language" style={{ whiteSpace: 'nowrap', paddingTop: '8px' }}>
				言語を選択：
			</label>
			<div
				onMouseEnter={handleMouseEnter}
				onMouseLeave={handleMouseLeave}
				style={{ position: 'relative', width: '200px' }}
			>
				<div
					style={{
						padding: '8px',
						border: '1px solid #ccc',
						borderRadius: '4px',
						background: '#fff',
						cursor: 'pointer',
					}}
				>
					{selected.label}
				</div>

				<div
					style={{
						position: 'absolute',
						top: '100%',
						left: 0,
						right: 0,
						background: '#fff',
						border: '1px solid #ccc',
						borderTop: 'none',
						borderRadius: '0 0 4px 4px',
						overflow: 'hidden',
						maxHeight: isOpen ? '240px' : '0',
						opacity: isOpen ? 1 : 0,
						transform: isOpen ? 'scaleY(1)' : 'scaleY(0)',
						transformOrigin: 'top',
						transition: 'all 0.3s ease-out',
						zIndex: 10,
					}}
				>
					{options.map((option) => (
						<div
							key={option.value}
							onClick={() => handleSelect(option)}
							style={{
								padding: '8px',
								cursor: 'pointer',
								backgroundColor: selected.value === option.value ? '#f0f0f0' : 'transparent',
								transition: 'background-color 0.2s',
							}}
							onMouseEnter={(e) => {
								if (selected.value !== option.value) {
									e.currentTarget.style.backgroundColor = '#f0f0f0';
								}
							}}
							onMouseLeave={(e) => {
								if (selected.value !== option.value) {
									e.currentTarget.style.backgroundColor = 'transparent';
								}
							}}
						>
							{option.label}
						</div>
					))}
				</div>
			</div>
		</div>
	);
};

export default AnimatedSelect;

```
