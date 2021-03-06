##Vanilla 的 controller
*vanilla 的 controller 是业务处理的关键，基本的用法请参考 [快速开始](../quick_learning/add_controller.md)。*

###*关于 Controller*
*Vanilla 的 Controller 可以是任何普通的 LUA 包，只不过导入的方法被用作处理请求的 Action。如下示例：*

```lua
local IndexController = {}

-- curl http://localhost:9110
function IndexController:index()
    local view = self:getView()
    local p = {}
    p['vanilla'] = 'Welcome To Vanilla...' .. user_service:get()
    p['zhoujing'] = 'Power by Openresty'
    -- view:assign(p)
    do return view:render('index/index.html', p) end
    return view:display()
end

-- curl http://localhost:9110/index/action_b
function IndexController:action_b()
    return 'index->action_b'
end

return IndexController
```

###*更面向对象的 Controller*
*Vanilla 支持使用 `Class` 方法来声明一个 Controller，实例如下：*

```lua
local IndexController = Class('controllers.index')

-- curl http://localhost:9110/index/action_b
function IndexController:action_b()
    return 'index->action_b'
end

return IndexController
```

*这种情况下，可以定义 Controller 的构造器来对其进行初始化。示例如下：*

```lua
local IndexController = Class('controllers.index')

function IndexController:__construct()
    self.aa = aa({info='ppppp'})
end

-- curl http://localhost:9110/index/action_b
function IndexController:action_b()
    return 'index->action_b'
end

return IndexController
```

*甚至还可以声明一个 Controller 基类，处理某些通用的逻辑，相关的详细用法参见 Vanilla[面向对象](../advanced/oo.md) 相关章节。*