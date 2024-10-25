<%*
async function getUserInputAndOptions() {
    try {
        // 获取文件名称并重命名
        const input = await tp.system.prompt("请输入文件名称");
        const currentDate = tp.date.now("YYYY-MM-DD");
        await tp.file.rename(`${currentDate}-${input}`);
        
        // 使用 moment.js (Templater内置) 格式化当前日期时间
        const currentDateTime = moment().format("YYYY-MM-DD HH:mm:ss");

        // 获取文章标题
        const titleInput = await tp.system.prompt("请输入文章 title");
        if (!titleInput) {
            throw new Error("文章标题不能为空");
        }

        // 获取分类
        const categoriesInput = await tp.system.prompt("文章分类，最多两个以英文逗号分隔");

        // 获取标签
        const tagsInput = await tp.system.prompt("文章标签，多标签以英文逗号分隔");

        // 获取 description
        const descriptionInput = await tp.system.prompt("自定义文章说明，不填写网站自动显示");

        // 获取 image
        const imageInput = await tp.system.prompt("该文章图片位置-自定义");

        // 获取 media_subpath
        const mediaSubpathInput = await tp.system.prompt("该文章图片所在目录-自定义");

        // 定义是否置顶的选项列表
        const pinOptions = {
            "文章置顶": true,
            "文章不置顶": false
        };

        // 生成提示模式并返回用户的选择
        const pinKeys = Object.keys(pinOptions);
        const pinChoice = await tp.system.suggester(pinKeys, pinKeys);
        const pinValue = pinOptions[pinChoice];

        // 定义作者选项列表
        const authorOptions = {
            "作者：星霜": "xingshuang",
            "作者：晓白": "晓白",
            "作者：xiaobai": "xiaobai"
        };

        // 生成作者提示模式并返回用户的选择
        const authorKeys = Object.keys(authorOptions);
        const authorChoice = await tp.system.suggester(authorKeys, authorKeys);
        const authorValue = authorOptions[authorChoice];

        // 定义 license 选项列表
        const licenseOptions = {
            "该文章使用特别说明-版权": true,
            "该文章不使用特别说明-版权": false
        };
        const licenseKeys = Object.keys(licenseOptions);
        const licenseChoice = await tp.system.suggester(licenseKeys, licenseKeys);
        const licenseValue = licenseOptions[licenseChoice];

        // 定义 math 选项列表
        const mathOptions = {
            "文章开启数学公式": true,
            "文章不开启数学公式": false
        };
        const mathKeys = Object.keys(mathOptions);
        const mathChoice = await tp.system.suggester(mathKeys, mathKeys);
        const mathValue = mathOptions[mathChoice];

        // 定义 render_with_liquid 选项列表
        const renderWithLiquidOptions = {
            "使用liquid渲染": true,
            "不使用使用liquid渲染": false
        };
        const renderWithLiquidKeys = Object.keys(renderWithLiquidOptions);
        const renderWithLiquidChoice = await tp.system.suggester(renderWithLiquidKeys, renderWithLiquidKeys);
        const renderWithLiquidValue = renderWithLiquidOptions[renderWithLiquidChoice];

        // 定义 published 选项列表
        const publishedOptions = {
            "已发布": true,
            "未发布": false
        };
        const publishedKeys = Object.keys(publishedOptions);
        const publishedChoice = await tp.system.suggester(publishedKeys, publishedKeys);
        const publishedValue = publishedOptions[publishedChoice];

        return { 
            titleInput, 
            categoriesInput, 
            tagsInput, 
            pinValue, 
            authorValue, 
            licenseValue, 
            mathValue, 
            descriptionInput, 
            renderWithLiquidValue, 
            publishedValue,
            currentDateTime,
            imageInput,
            mediaSubpathInput
        };
    } catch (error) {
        console.error(`获取用户输入失败: ${error.message}`);
        throw error;
    }
}

function generateFrontMatter(data) {
    const frontMatter = [
        '---',
        `title: ${data.titleInput}`,
        `date: ${data.currentDateTime} +0800`,
        `categories: [${data.categoriesInput}]`,
        `tags: [${data.tagsInput}]`
    ];

    if (data.pinValue) frontMatter.push('pin: true');
    if (data.imageInput) frontMatter.push(`image: ${data.imageInput}`);
    if (data.mediaSubpathInput) frontMatter.push(`media_subpath: ${data.mediaSubpathInput}`);
    if (data.authorValue) frontMatter.push(`author: ${data.authorValue}`);
    if (data.licenseValue!== undefined) frontMatter.push(`license: ${data.licenseValue}`);
    if (data.mathValue!== undefined) frontMatter.push(`math: ${data.mathValue}`);
    if (data.descriptionInput) frontMatter.push(`description: ${data.descriptionInput}`);
    if (data.renderWithLiquidValue!== undefined) frontMatter.push(`render_with_liquid: ${data.renderWithLiquidValue}`);
    if (data.publishedValue!== undefined) frontMatter.push(`published: ${data.publishedValue}`);

    frontMatter.push('---\n');
    return frontMatter.join('\n');
}

// 获取用户输入并生成front matter
const data = await getUserInputAndOptions();
const frontMatter = generateFrontMatter(data);

try {
    const targetPath = "/_posts/" + `${currentDate}`;
    await tp.file.move(`${targetPath}`);
} catch (error) {
    console.error(`文件移动失败: ${error.message}`);
}
// 返回生成的内容
return frontMatter;
-%>
