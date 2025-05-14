#include <gtk/gtk.h>

// Function called when the Start button is clicked
static void on_start_button_clicked(GtkWidget *widget, gpointer data) {
    g_print("Simulation started!\n");
}

int main(int argc, char *argv[]) {
    GtkWidget *window, *grid;
    GtkWidget *label, *entry, *combo, *button;

    gtk_init(&argc, &argv);

    // Create window
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_window_set_title(GTK_WINDOW(window), "Trade Simulator");
    gtk_window_set_default_size(GTK_WINDOW(window), 600, 400);
    g_signal_connect(window, "destroy", G_CALLBACK(gtk_main_quit), NULL);

    // Create grid and attach to window
    grid = gtk_grid_new();
    gtk_container_add(GTK_CONTAINER(window), grid);

    // Exchange
    label = gtk_label_new("Exchange:");
    entry = gtk_entry_new();
    gtk_entry_set_text(GTK_ENTRY(entry), "OKX");
    gtk_grid_attach(GTK_GRID(grid), label, 0, 0, 1, 1);
    gtk_grid_attach(GTK_GRID(grid), entry, 1, 0, 1, 1);

    // Asset
    label = gtk_label_new("Spot Asset:");
    entry = gtk_entry_new();
    gtk_entry_set_text(GTK_ENTRY(entry), "BTC-USDT");
    gtk_grid_attach(GTK_GRID(grid), label, 0, 1, 1, 1);
    gtk_grid_attach(GTK_GRID(grid), entry, 1, 1, 1, 1);

    // Order Type
    label = gtk_label_new("Order Type:");
    combo = gtk_combo_box_text_new();
    gtk_combo_box_text_append_text(GTK_COMBO_BOX_TEXT(combo), "Market");
    gtk_combo_box_set_active(GTK_COMBO_BOX(combo), 0);
    gtk_grid_attach(GTK_GRID(grid), label, 0, 2, 1, 1);
    gtk_grid_attach(GTK_GRID(grid), combo, 1, 2, 1, 1);

    // Quantity
    label = gtk_label_new("Quantity (USD):");
    entry = gtk_entry_new();
    gtk_entry_set_text(GTK_ENTRY(entry), "100");
    gtk_grid_attach(GTK_GRID(grid), label, 0, 3, 1, 1);
    gtk_grid_attach(GTK_GRID(grid), entry, 1, 3, 1, 1);

    // Volatility
    label = gtk_label_new("Volatility (%):");
    entry = gtk_entry_new();
    gtk_entry_set_text(GTK_ENTRY(entry), "1.0");
    gtk_grid_attach(GTK_GRID(grid), label, 0, 4, 1, 1);
    gtk_grid_attach(GTK_GRID(grid), entry, 1, 4, 1, 1);

    // Fee Tier
    label = gtk_label_new("Fee Tier:");
    combo = gtk_combo_box_text_new();
    gtk_combo_box_text_append_text(GTK_COMBO_BOX_TEXT(combo), "Tier 1");
    gtk_combo_box_text_append_text(GTK_COMBO_BOX_TEXT(combo), "Tier 2");
    gtk_combo_box_text_append_text(GTK_COMBO_BOX_TEXT(combo), "Tier 3");
    gtk_combo_box_set_active(GTK_COMBO_BOX(combo), 0);
    gtk_grid_attach(GTK_GRID(grid), label, 0, 5, 1, 1);
    gtk_grid_attach(GTK_GRID(grid), combo, 1, 5, 1, 1);

    // Start Button
    button = gtk_button_new_with_label("Start Simulation");
    g_signal_connect(button, "clicked", G_CALLBACK(on_start_button_clicked), NULL);
    gtk_grid_attach(GTK_GRID(grid), button, 0, 6, 2, 1);

    gtk_widget_show_all(window);
    gtk_main();

    return 0;
}
