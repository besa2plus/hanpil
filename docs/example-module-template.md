# Example Module Template

이 문서는 hanpil Module 개발을 위한 간단한 템플릿 예시입니다.

## 디렉토리 구조 (예시)

```
my-awesome-module/
├── metadata.ts          # 또는 metadata.json / __init__.py 등
├── index.ts             # 또는 main.py
├── types.ts
└── README.md
```

## metadata 예시 (TypeScript Module)

```ts
export const metadata = {
  name: 'my-awesome-module',
  description: '멋진 기능을 제공하는 EMP Module 예시',
  version: '0.1.0',
  author: '@yourname',
  contributors: [],
  language: 'typescript',
  package_manager: 'pnpm',
  install_command: 'pnpm install',
  runtime_requirements: ['node>=20'],
  entry_point: 'index.ts',
  dependencies: []
};
```

## metadata 예시 (Python + uv Module)

```python
metadata = {
    "name": "my-awesome-module",
    "description": "Python으로 작성된 EMP Module",
    "version": "0.1.0",
    "author": "@yourname",
    "language": "python",
    "package_manager": "uv",
    "install_command": "uv sync",
    "runtime_requirements": ["python>=3.11"],
    "entry_point": "main.py",
}
```

## PR 시 체크 포인트

- 500줄 이하 유지
- metadata에 language/package_manager 포함
- Engine이 install_command를 실행할 수 있도록 정확히 작성

이 템플릿을 기반으로 실제 Module을 개발한 후 Registry에 등록하세요.
