{
  "format_version": "1.10",
  "header": {
    "description": "Custom Home Screen with Elite King",
    "name": "Elite King Pack",
    "uuid": "unique-identifier-for-your-resource-pack",
    "version": [1, 0, 0]
  },
  "modules": [
    {
      "description": "Custom Home Screen",
      "type": "resources",
      "uuid": "unique-identifier-for-your-module",
      "version": [1, 0, 0]
    }
  ]
}
public class ExampleMod extends BaseMod {

    @Override
    public void onInitialize() {
        // Register a keybind to open the GUI
        KeyBindingRegistry.INSTANCE.registerKeyBinding(new KeyBinding(
                "Open GUI",
                InputUtil.Type.KEYSYM,
                GLFW.GLFW_KEY_G,
                "ExampleMod"
        ));

        // Register a client-side event listener
        ClientTickEvents.END_CLIENT_TICK.register(client -> {
            while (KeyBindingRegistry.INSTANCE.wasPressed(new KeyBinding("Open GUI", InputUtil.Type.KEYSYM, GLFW.GLFW_KEY_G, "ExampleMod"))) {
                // Open the GUI when the keybind is pressed
                MinecraftClient.getInstance().openScreen(new ExampleScreen());
            }
        });
    }

    public static class ExampleScreen extends HandledScreen<ExampleScreenHandler> {

        public ExampleScreen() {
            super(new ExampleScreenHandler());
        }

        @Override
        protected void init() {
            super.init();
            // Add GUI components here (buttons, labels, etc.)
        }

        @Override
        public void render(MatrixStack matrices, int mouseX, int mouseY, float delta) {
            this.renderBackground(matrices);
            super.render(matrices, mouseX, mouseY, delta);
            this.drawMouseoverTooltip(matrices, mouseX, mouseY);
        }
    }

    public static class ExampleScreenHandler extends ScreenHandler {
        // Implement your screen handler logic here
    }
}
