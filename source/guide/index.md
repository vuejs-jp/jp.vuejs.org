title: Getting Started
type: guide
order: 2
---

## Introduction

Vue.js �̓C���^���N�e�B�u�ȃE�F�u�C���^�[�t�F�[�X����邽�߂̃��C�u�����[�ł��B

�Z�p�I�ɁAVue.js ��MVVM pattern �� [ViewModel](#ViewModel) layer �ɒ��ڂ��Ă��܂��B[ViewModel](#ViewModel) layer �͑o�����o�C���f�B���O�ɂ���� [View](#View) �� [Model](#Model) ��ڑ����܂��B���ۂ� DOM ����Əo�͂̌`����[Directives](#Directives) �� [Filters](#Filters)�ɂ���Ē��ۉ�����Ă��܂��B

Vue.js �̓N�w�I�ȃS�[���́A�\�Ȍ���ȒP��API��ʂ��āA�������̗ǂ��f�[�^�o�C���f�B���O�̗��_�ƍ\���\��view�̃R���|�[�l���g��񋟂��邱�Ƃł��BVue.js�͖��\�ȃt���[�����[�N�ł͂���܂���B Vue.js�͒P�������R���݂�view layer�ɂȂ�悤�Ƀf�U�C������Ă��܂��BVue.js��P�̂Ń��s�b�h�v���g�^�C�s���O���ł��܂��B���ʂ� front-end stack �p�̃��C�u�����[�B�ƈꏏ�Ɏg������g�ݍ��킹������ł��܂��BVue.js�� Firebase �̂悤�ȃm�[�o�b�N�G���h�T�[�r�X�Ƃ��������ǂ��ł��B

Vue.js �� API �� [AngularJS]�A[KnockoutJS]�A[Ractive.js]�A [Rivets.js]�ɋ����e�����󂯂Ă��܂��B�����Ǝ��Ă͂��܂����A�P�����Ƌ@�\���̂��傤�Ǘǂ��X�B�[�g�X�|�b�g�������邱�Ƃɂ���āAVue.js�͂����̃��C�u�����[�ɑ΂��ĉ��l�����ώ�i�ɂȂ肤��Ǝ��͐M���Ă��܂��B

�M���́A���̑��̃��C�u�����[�̕\���Ɋ��Ɋ���Ă��邩������܂��񂪁A�����̕\���̋L�@��Vue.js �̕����ɂ����ĈӖ�����Ƃ���Ƃ͈���Ă��邩������܂���̂ŁA�ȉ��Ɏ����R���Z�v�g�̑S�̑��ɖڂ�ʂ��Ă݂Ă��������B

## Concepts Overview

### ViewModel

Model �� View�𓯊�����I�u�W�F�N�g�B Vue.js �ɂ�����, �S�Ă� Vue �C���X�^���X��ViewModel�ł��B ������ `Vue` �R���X�g���N�^�[�����̃T�u�N���X�ŃC���X�^���X������܂�:

```js
var vm = new Vue({ /* options */ })
```

����͋M����Vue.js�������ĊJ������Ƃ��ɏ��߂ďo��I�u�W�F�N�g�ł��B�ڍׂ� [The Vue Constructor](/api/) �����Ă��������B

### View

Vue �C���X�^���X�ɂ���ĊǗ��������ۂ� DOM.

```js
vm.$el // The View
```

Vue.js �� DOM �x�[�X�̃e���v���[�e�B���O���g���܂��B�e�X��Vue �C���X�^���X��associated with a �Ή����� DOM �v�f�Ɗ֘A�Â��Ă��܂��BVue �C���X�^���X�������ƁA�K�v�ȃf�[�^�o�C���f�B���O��ݒ肵�Ă���ԁAVue �C���X�^���X�͂��̐e�v�f�̑S�Ă̎q�m�[�h���ċA�I�ɏ��񂵂܂��B

Vue.js���g���Ă���Ƃ��ɁA�M�����M�����g��DOM �ɐG��邱�Ƃ�custom directives (��q)�������Ėw�ǂ���܂���B View �̍X�V�̓f�[�^���ς�����Ƃ��Ɏ����I�ɍs���܂��B������View �̍X�V�́AtextNode�Ɏ��鐸�x���������������x�i�H�j�ōs���܂��B �����͍����\���̂��߂ɁA�o�b�`������Ĕ񓯊����s����Ă����܂��B

### Model

�኱�C�����ꂽ�v���[���� JavaScript �I�u�W�F�N�g�B

```js
vm.$data // The Model
```

Vue.js�ɂ����āAModel �͒P���Ƀv���[���� JavaScript �I�u�W�F�N�g��**data objects**�ł��B�M���͂����̃v���p�e�B�ƁA����炪�ύX����邩���ώ@���Ă���Vue �C���X�^���X�𑀍�ł��܂��BVue.js ��data objects�̃v���p�e�B��ES5 getter/setters�ɕϊ����邱�Ƃɂ���āA���ߓI�ȉ����i�H�j���������܂��B �_�[�e�B�[�`�F�b�N�͕K�v����܂��񂵁AView���X�V���邽�߂ɁA�����I�ȃV�O�i���� Vue �ɑ���K�v������܂���B �f�[�^���ύX���ꂽ�Ƃ��͂��ł��A���̃t���[����View�͍X�V����܂��B

Vue �C���X�^���X�́A����炪�ώ@���Ă��� data objects �̑S�Ẵv���p�e�B���v���L�V���Ă��܂��B ���̂��߁A��x�I�u�W�F�N�g `{ a: 1 }` ���ώ@�����΁A `vm.$data.a` ��`vm.a` �̗����������l��Ԃ��܂��B�܂��A`vm.a = 2` �ɐݒ肷��� `vm.$data` ���ς��܂�.

data objects�͓K���Ȉʒu�ŕω����܂��B���̂��߁A�Q�Ƃɂ���Ă�����ύX���邱�Ƃ́A`vm.$data` ��ύX���邱�ƂƓ������ʂ������Ă��܂�. ���̎����A������ Vue �C���X�^���X���f�[�^�̓����������ώ@���邱�Ƃ��\�ɂ��Ă��܂��B���L�����p�Ƃ��ẮA Vue �C���X�^���X�͏�����view�Ƃ��Ďg���邱�ƁAand externalize the data ����̃��W�b�N����藣�U�I��store layer�ɋ�̉����邱�Ɓi�H�j�A����������܂��B

�����ł̖��́A��x�ώ@���n�܂�����AVue.js �̓v���p�e�B�̐V�K�ǉ��ƍ폜�����o�ł��Ȃ����Ƃł��B
���̖�������邽�߂ɁA�ώ@���ꂽ�I�u�W�F�N�g��`$add` �� `$delete` ���\�b�h�Œǉ��폜����܂��B
### Directives

Vue.js �� DOM �v�f�ɂ��Ẳ��������邱�Ƃ�`���Ă��� �v���t�B�b�N�X�̂��� HTML ����

```html
<div v-text="message"></div>
```

������Here the div �v�f�� value�� `message` `v-text` directive�������Ă��܂��B �����Vue.js ���Adiv�� textContent ��Vue �C���X�^���X��`message` �v���p�e�B�Ɠ������Ă��邱�Ƃ��A�ۂ��Ă��邱�Ƃ�`���Ă��܂��B

Directive �͔C�ӂ� DOM ������J�v�Z�����ł��܂��B�Ⴆ�΁A`v-attr` �͗v�f�̑����𑀍삵�܂����A`v-repeat` �̓A���C�Ɋ�Â��ėv�f���N���[�����܂����A, `v-on` �̓C�x���g���X�i�[�𐏍s���܂��B�����͌�ɂ܂Ƃ߂܂��B

### Mustache Bindings

�M���̓e�L�X�g�Ƒ����̗����ɂ�����mustache-style �o�C���f�B���O���g�����Ƃ��ł��܂��B�����͓����ŁA`v-text`�f�B���N�e�B�u �� `v-attr` �f�B���N�e�B�u�ɖ|�󂳂�܂��B�Ⴆ��:

```html
<div id="person-{{id}}">Hello {{name}}!</div>
```

���̏������͕֗��ł����A���������ӂ��Ȃ���΂Ȃ�Ȃ����Ƃ�����܂�:

<p class="tip"> `<image>` �v�f�� `src` �����́A�l���ݒ肳�ꂽ�Ƃ���HTTP ���N�G�X�g���쐬���܂��B���̂��߁A�e���v���[�g�����߂ɉ�͂��ꂽ�Ƃ��ɁA404�̌��ʂ��Ԃ��Ă��܂�. ���̏ꍇ�́A`v-attr` ���g���̂��ǂ��ł��B </p>

<p class="tip">Internet Explorer �́AHTML����͂��Ă���Ƃ��ɁA`style`�����̖����ȃC�����C�����폜���܂��B ���̂���IE���T�|�[�g�������ꍇ�A �C�����C��CSS ���o�C���f�B���O����Ƃ��ɂ͂���`v-style`���g���Ă��������B</p>

�G�X�P�[�v����Ă��Ȃ��i�H�jHTML�ɑ΂���3�d��mustache���g�����Ƃ��ł��A����͓�����`v-html` �ɖ|�󂳂�܂�:

``` html
{{{ safeHTMLString }}}
```

�������Ȃ���Athis can open up windows for potential XSS attacks, therefore it is suggested that you only use triple mustaches when you are absolutely sure about the security of the data source, or pipe it through a custom filter that sanitizes untrusted HTML.

Finally, you can add `*` to your mustache bindings to indicate a one-time only interpolation, which does not react to data changes:

``` html
{{* onlyOnce }}
```

### Filters

Filters are functions used to process the raw values before updating the View. They are denoted by a "pipe" inside directives or bindings:

```html
<div>{{message | capitalize}}</div>
```

Now before the div's textContent is updated, the `message` value will first be passed through the `capitalize` function. For more details see [Filters in Depth](/guide/filters.html).

### Components

In Vue.js, every component is simply a Vue instance. Components form a nested tree-like hierarchy that represents your application interface. They can be instantiated by a custom constructor returned from `Vue.extend`, but a more declarative approach is registering them with `Vue.component(id, constructor)`. Once registered, they can be declaratively nested in other Vue instance's templates with the `v-component` directive:

``` html
<div v-component="my-component">
  <!-- internals handled by my-component -->
</div>
```

This simple mechanism enables declarative reuse and composition of Vue instances in a fashion similar to [Web Components](http://www.w3.org/TR/components-intro/), without the need for latest browsers or heavy polyfills. By breaking an application into smaller components, the result is a highly decoupled and maintainable codebase. For more details, see [Component System](/guide/components.html).

## A Quick Example

``` html
<div id="demo">
  <h1>{{title | uppercase}}</h1>
  <ul>
    <li
      v-repeat="todos"
      v-on="click: done = !done"
      class="{{done ? 'done' : ''}}">
      {{content}}
    </li>
  </ul>
</div>
```

``` js
var demo = new Vue({
  el: '#demo',
  data: {
    title: 'todos',
    todos: [
      {
        done: true,
        content: 'Learn JavaScript'
      },
      {
        done: false,
        content: 'Learn Vue.js'
      }
    ]
  }
})
```

**Result**

<div id="demo"><h1>&#123;&#123;title | uppercase&#125;&#125;</h1><ul><li v-repeat="todos" v-on="click: done = !done" class="&#123;&#123;done ? 'done' : ''&#125;&#125;">&#123;&#123;content&#125;&#125;</li></ul></div>
<script>
var demo = new Vue({
  el: '#demo',
  data: {
    title: 'todos',
    todos: [
      {
        done: true,
        content: 'Learn JavaScript'
      },
      {
        done: false,
        content: 'Learn Vue.js'
      }
    ]
  }
})
</script>

Also available on [jsfiddle](http://jsfiddle.net/yyx990803/yMv7y/).

You can click on a todo to toggle it, or you can open your Browser's console and play with the `demo` object - for example, change `demo.title`, push a new object into `demo.todos`, or toggle a todo's `done` state.

You probably have a few questions in mind now - don't worry, we'll cover them soon. Next up: [Directives in Depth](/guide/directives.html).

[AngularJS]: http://angularjs.org
[KnockoutJS]: http://knockoutjs.com
[Ractive.js]: http://ractivejs.org
[Rivets.js]: http://www.rivetsjs.com
