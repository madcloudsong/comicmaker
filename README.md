# ComicMaker - 漫剧视频创作工具

一个基于 AI 的漫剧视频创作工具，支持素材管理、剧集创建、分镜生成和内容生成。

注：个人使用OpenSpec按照自己写的需求定义的一个toy，仅供交流学习，真正投入生产还需要做很多优化。

## 功能特性

### 素材管理
- **人物角色管理**：创建、编辑、删除人物角色素材
- **场景管理**：创建、编辑、删除场景素材
- **道具管理**：创建、编辑、删除道具素材

### 剧集管理
- **作品管理**：创建和管理漫剧作品
- **剧集管理**：为每个作品创建多个剧集
- **分镜生成**：从脚本自动生成分镜脚本
- **内容生成**：生成图片、视频、音频
- **预览功能**：预览完整的剧集

## 技术栈

- **前端**：HTML + JavaScript + CSS（原生 Web 技术）
- **后端**：Python + FastAPI
- **数据存储**：JSON 文件 + 文件系统

## 安装和运行

### 后端服务

1. 安装依赖：
```bash
cd server
pip install -r requirements.txt
```

2. 启动服务：
```bash
python main.py
```

服务将在 `http://localhost:8000` 启动

### 运行测试

1. 确保后端服务已启动
2. 运行测试：
```bash
cd server
python -m pytest tests/              # 运行所有测试
python tests/run_tests.py            # 使用测试脚本
```

或访问 Web 测试界面：`http://localhost:8080/test-api.html`

### 前端页面

1. 使用简单的 HTTP 服务器打开前端页面：
```bash
cd apps/web
python -m http.server 8080
```

2. 在浏览器中访问 `http://localhost:8080`

## 项目结构

```
comicmaker/
├── apps/
│   └── web/              # 前端页面
│       ├── index.html
│       ├── materials.html
│       ├── works.html
│       ├── styles/
│       └── js/
├── server/               # 后端服务
│   ├── main.py          # FastAPI 主应用
│   ├── api/             # API 路由
│   │   ├── materials.py
│   │   ├── works.py
│   │   ├── episodes.py
│   │   └── content.py
│   └── utils.py         # 工具函数
└── data/                # 数据存储目录（自动创建）
    ├── materials/       # 素材资源
    └── works/           # 作品和剧集
```

## API 文档

启动后端服务后，访问 `http://localhost:8000/docs` 查看自动生成的 API 文档。

## 使用说明

1. **素材管理**：
   - 进入"素材管理"页面
   - 选择素材类型（人物角色/场景/道具）
   - 点击"创建新素材"添加素材
   - 上传主图和可选的辅助图片
   - 填写名称和描述

2. **创建作品**：
   - 进入"作品管理"页面
   - 点击"创建新作品"
   - 填写作品名称和描述
   - 编辑作品详情（封面、风格、宽高比等）

3. **创建剧集**：
   - 在作品列表中点击"编辑剧集"
   - 点击"创建新剧集"
   - 填写剧集名称和描述

4. **编辑剧集**：
   - 在剧集列表中点击"编辑剧集"
   - 输入脚本内容
   - 点击"生成分镜脚本"
   - 为每个分镜生成图片、视频、音频
   - 点击"预览剧集"查看效果

## 注意事项

- 内容生成功能（图片、视频、音频）需要配置相应的 AI API
- 当前实现中，内容生成部分返回示例数据，需要集成实际的 AI 服务
- 数据存储在 `data/` 目录中，请确保有写入权限

- server/config/config.yaml里的一些ai的key需要填上，比如生图生视频我用的wavespeed的封装api，之前研究一个agent项目时看别人用的，wavespeed_api字段要填上key。
- LLM的我用的openrouter的封装api，访问gpt方便一些，填在openai_api_key字段上。
- 以及阿里云oss的key和bucket，需要开公共读，用来做图床，给一些图和视频模型用来访问图的，内在代码逻辑是先上传到oss，然后把链接给到生图生视频接口。

## 开发计划

- [ ] 集成 LLM API 用于分镜生成
- [ ] 集成 Text-to-Image API
- [ ] 集成 Text-to-Video API
- [ ] 集成 TTS API 用于音频生成
- [ ] 添加历史记录浏览功能
- [ ] 优化预览功能

